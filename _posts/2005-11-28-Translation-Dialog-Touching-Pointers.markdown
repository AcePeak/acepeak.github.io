---
layout: blogs_item
title: 【翻译】对话：接触指针
author: AcePeak
categories:
  - 积累
tags:
  - C++
  - boost
  - 原创
---

“哎呀！”

这是我一小时内第七次受挫了。显然Wendy很讨厌我这样。“看就看吧，朋友，安静一会行不行？”她的声音飘出了隔间。貌似比她先前的反应好些。

我正是在auto_ptrs这里摔跤了。在为Guru工作的前些天里，我已经了解了auto_ptrs的好处-以及他们并不很明显的缺陷。我已经被auto_ptrs的奇怪的所有权语义刺痛了。auto_ptr是用move操作来代替copy操作，想象一下：当你走近一台影印机，把材料放进进纸器，按下“Copy”按钮。几分钟之后，影印机给了你一份拷贝-然后把原文扔进了碎纸机。这正好和auto_ptr的拷贝和赋值做的一样。

总之，虽然我很聪明还有更多的经验，我仍然撞在了auto_ptr的各种限制上面。auto_ptr不能持有指向数组的指针， 我打算通过以下删除数组的方式来玩玩它：


{% highlight C++ %}
auto_ptr<T> autoArray(new T[10]);
//...
delete [] autoArray.release();
{% endhighlight %}


但是我几乎马上抛弃了这个主意。甚至我可以看到这个“憎恶（abomination）（正如Guru说的）”的很多危害。全部的，恩，全部的auto_ptr的要点都是用于拥有和销毁内存的；要是手动处理就完全违背了其目的。

因此我决定使用vector来取代拥有一个array， 这将比我需要的更强大，因为我不需要vector的动态调整大小，但它却符合我的目的。我真正想要的是一个能自动持有指针和内存管理权的智能指针，来让我可以用来操作一个数组。

“使用Boost， Luke，”我听到了背后Guru的声音。

“不是“使用Force，Luke”吗？”我耸耸肩，“还有，不要叫我Luke。”

“Boost库将是一个强大的支持，”Guru继续她的完美表演。

虽然我今天不在状态，但我仍打断了她。“阿，我们今天能不能不要表演了？Bob在我们伦敦的办公室，没有实习医生可以处理反常者了。”

她来到我旁边，我看到她笑着耸了耸肩，“哦，我刚才觉得很无聊，”她叹了口气，“你检验过Boost库的智能指针了吗？”

“唔，好吧，”我犹豫了，“我还没机会看Boost库的细节。使用智能指针方法的都有什么？”

“总共有5种，”Guru坐下后说。“2个提供了简单指针所有权，2个共享所有权。”

“共享所有权？哦，就是说像一个引用技术类咯？”

“没错，智能指针是成对的，所以你有一个持有指向简单对象的指针的智能指针的时候，还有一个持有指向数组的指针。”她突然停住了，开始在白板上写下了：scoped_ptr, scoped_array, shared_ptr, shared_array。

“这只有4个；你不是说有5个吗？”我质问。

“还有一个是weak_ptr。它是shared_ptr的一个无所有权的观察者。我待会会说到这个。scoped_* 指针自动销毁超出作用区域的对象， 一种建议的用法就是实现出Pimpl-指向实现的，”她一口气说完，阻止了我另一次的双关语。

“那么。。。他们都像auto_ptr，对吗？”

“不全是。scoped_ptr和scoped_array是不可以拷贝的。”

“不可以拷贝？那么，如果我有一个作为类的成员-”我拿起笔说，开始在白板上涂写：


{% highlight C++ %}
 class T
{
scoped_ptr<TImpl> p;
...
{% endhighlight %}


“-我如何实现拷贝和赋值呢？”

“就跟使用auto_ptr是一样，”Guru回答，然后她写了：


{% highlight C++ %}
T( const T& other):p(new TImpl(*other.p))
{
}
T &operator=(const T& other)
{
    scoped_ptr<TImpl> tmp(new TImpl(*other.p));
    p.swap(tmp);
}
{% endhighlight %}


“好吧，”我一边消化这种用法一边懒洋洋的说，“那么，当我在用scoped_ptr时,我必须做和用auto_ptr一样的工作，是吗？那么为什么不直接用auto_ptr？”

“因为使用auto_ptr会为了自动生成的函数编译，这并不是在做坏的事情。使用scoped_ptr使它更难发生意外无意的拷贝语义，因为如果你用编译器生成的版本的话，编译器会拒绝编译这个类。 还有，scoped_ptr不能被用在一个不完整的类型上。”我有点不知所措的看向Guru。她叹了口气，“比如这样，”她边说边在白板上写：


{% highlight C++ %}
class Simple;
Simple* CreateSimple();
void f()
{
  auto_ptr<Simple> autoS(CreateSimple());
  scoped_ptr<Simple> scopedS(CreateSimple());
  //...
}
{% endhighlight %}


“在这个函数里，Simple是一个不完整的类型。如果析构需要代价，那么通过auto_ptr或者scoped_ptr析构就会导致未定义的行为。当你实例化一个auto_ptr时，一些编译器会警告你，但不全是这样。另一面，scoped_ptr，如果实例化一个不完整的类型，在那之前就会产生一个编译错误。”

“哦，对，当然如此，”我插了进来，以表明我明白这点。“那么我们总可以使用scoped_ptr来取代auto_ptr,是不是？”

“对不起，错，”她说道，很失望。“auto_ptr仍然有自己的用处。跟auto_ptr不一样，scoped_ptr没有release()成员-也就是说它不能放弃指针的所有权。正因为如此，还因为scoped_ptr不能拷贝，当scoped_ptr出了范围的时候，它所管理的指针总会被删除。这是scoped_ptr不适合于那些你真正需要传递所有权的场合，比如工厂。

“使用scoped_ptr把你的意图发给其他程序员。它告诉他们：‘这个指针不应该在当前范围外被拷贝。’另一方面，auto_ptr授权可以在创建指针的范围外传播所有权，但是在所有权传播完成后，它仍然还可以控制指针。当然，这在写异常-安全(exception-safe)的代码时很重要。”

“阿，好吧，我知道了，”我咕哝着，“其他你提到的智能指针呢？”

“scoped_array就像一个scoped_ptr，只是它管理一个对象数组而不是一个简单对象。scoped_array提供了一些稍为不同的访问函数。它并没有*和->操作符，但是它有[]操作符。 我相信，”她总结说，“你需要的智能指针是一个scoped_array指针。”

“也许吧，”我回答，“但是我想在我决定之前我还想对这些shared_*智能指针多了解一些。”

“很好，我的学...徒，对不起，我失口了。”Guru羞涩的对我笑了笑。“是的，在决定之前对所有的选择都熟悉一下是一个好的工程实践（？）。”

“shared_*智能指针呢，”她指了指白板上的shared_ptr和shared_array，“是很强大的工具。他们是引用计数的指针，他们能区分拥有者和观察者。比如，使用下面这个类T：”


{% highlight C++ %}
void sharing()
{
  shared_ptr<T> firstShared(new T);
  shared_ptr<T> secondShared(firstShared);
  //...
}
{% endhighlight %}


“2个shared_ptr对象都指向相同的T对象。shared_ptr的使用计数现在是2。由于shared_ptr被引用计数了，对象在最后一个shared_ptr出了作用范围-引用计数降到0-才会销毁。

“shared_*指针非常有弹性，因此你可以使用他们来持有指向不完整类型的指针。”

“我记得你刚说这样不好？”

“如果不注意使用的话，这样确实并不好。但是只要你指定一个当持有的对象被销毁时候会调用的函数或者函数对象，shared_*指针就能用一个指向不完整类型的指针实例化出来。比如，如果我们修改了我们上面的小函数f：”


{% highlight C++ %}
void DestroySimple(Simple*);
void f()
{
  shared_ptr<Simple> sharedSFails(CreateSimple());
  shared_ptr<Simple> sharedSSucceeds(CreateSimple(), DestroySimple);
}
{% endhighlight %}


“第一个shared_ptr失败了，因为Simple是一个不完整的类型。第二个成功了，因为你已经无二义的告诉shared_ptr如何销毁这个指针。

“因为shared_ 指针被设计用来拷贝的，他们都很适合用在标准容器中，包括关联容器。而且，在那些需要转换的仅有的情况下，还有特殊操作符定义出来，这些操作符创建一个新的shared_* 指针。 比如，如果我们在明显的公有继承体系中有类Base 和 Derived和一个无关联的类，我们可以这样：”


{% highlight C++ %}
void g()
{
  shared_ptr<Base> sharedBase(new Derived);
  shared_ptr<Derived> sharedDer = shared_dynamic_cast<Derived>(sharedBase);
  shared_ptr<Unrelated> sharedDer = shared_dynamic_cast<Unrelated>(sharedBase);
  try
  {
     shared_ptr<Unrelated> oops = shared_polymorphic_cast<Unrelated>(sharedBase);
  }
  catch(bad_cast)
  {
     //...
  }
}
{% endhighlight %}


“还有一个shared_static_cast，是用在需要的极少的场合的，”Guru总结道。

我研究了这个函数一会。“好吧，我看看我是否能遵循这些。第一个shared_dynamic_cast执行针对智能指针的dynamic_cast并且返回一个新的智能指针。如果dynamic_cast失败了，引用计数将会怎样？”

Guru赞许的点点头。“那样的话，原始的计数将不受影响，新的shared_ptr将包含一个NULL指针。你也许能从try/catch子句推出来，shared_polymorphic_cast也会尝试对拥有的指针执行dynamic_cast。如果转换失败，就会抛出一个bad_cast异常。”

“喔，”我暗暗叫绝，“这才是那个类。看起来真是为此而设计的。”

“确实，”Guru也同意。“但是还有2件事要注意。引用计数很简单，但不能检测循环引用。还有，shared_ptr不能实现写方式的拷贝形式，因此如果要实现Pimpl，你必须多加小心。”

我对它捉摸了半天，发现我很喜欢它。“嘿，”我想起来什么，又说，“那么你提到的weak_ptr呢？”

“阿，是的。weak_ptr用于关联shared_ptr。weak_ptr是一个观察者，它并不影响共享对象的使用计数。weak_ptr的主要目的是用来允许shared_ptr参与到循环依赖中来-A持有B的引用，B同时也持有A的引用。我更喜欢把weak_ptr当作一个俱乐部中的关联成员-它没有投票权，但是可以参加俱乐部活动。”

“呒...”我想了一会。“因为weak_ptr没有影响使用计数，当weak_ptr在用一个共享对象，此时如果俱乐部解散-换句话说，最后一个shared_ptr出了范围-会发生什么事呢？”

“那样的话，weak_ptr管理的指针会被设置为NULL。讲到NULL，没有可以卸领（dereferencing）的操作符，比如*，-〉，[]，会在卸领之前检查一个NULL指针。因此，正如你所指出的在卸领之前原始指针非空，你还必须检查一个智能指针不为空。这个限制也适用于Boost库中所有的智能指针。”

“老大，有太多的材料要记了，”我说着，看着我自己潦草的白板。

“别担心，”Guru笑道，准备站起来走了。“我会发email给你Boost精简库的网址和一个小程序，它可以用来练习和示例各种指针。”当然，她对自己的话从不食言，几分钟后我收到了她的email。我揉了揉我的眼睛，因为我只看到：

“我的小学徒，这儿是那个Boost文章的地址：<[www.boost.org/libs/smart_ptr/smart_ptr.htm](www.boost.org/libs/smart_ptr/smart_ptr.htm)>。看看它，再思考一下附件中关于谦虚的寓言。”
