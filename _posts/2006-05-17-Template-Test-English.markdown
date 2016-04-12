---
layout: blogs_item
title: C++ Template 习题
author: AcePeak
categories:
  - 积累
tags:
  - C++
  - Template
  - 试题
  - 原创
---

{% highlight C++ %}
//
//因为这次公司培训机制改变为先发布题目，由学员看书做题，再由教员专向辅导。
//因此这次没有准备讲义，只把题目贴上来，朋友们也可以练练手，过几天把部分答案上传。
//本套题分为四个难度：BASE, ADVANCED, EXPLORATION, FUN. 思考难度指数分别大概是
//2，5，7，9（满分10）。其中BASE和ADVANCED是要求学员一定要做的。EXPLORATION
//是探索题目，FUN是探索题目做完后还有余力的一些很有意思有嚼头的题目。
//
//PS:自我感觉题目总体难度有些高，不知道学员能不能坚持下来...

//这里想要放一个目录链接到一下各个section的，但是不知道怎么做，有朋友知道的能说说吗？
{% endhighlight %}

BASE:
1． write the output.

{% highlight C++ %}
template<class Type>
void Func(Type &x , Type &y)
{
    Type a=x;
    x=y;
    y=a;
}

#include <iostream>
using namespace std;

int main()
{
    int a = 12;
    int b = 24;
    Func(a,b);
    cout<<"a:"<<a<<" "<<"b:"<<b<<endl;
}
{% endhighlight %}


2． With the function Template:

{% highlight C++ %}
template<int size , class T >
void Show(T *d)
{
    for( int j=0;j<size;j++)
        cout<<d[j]<<' ';
}
{% endhighlight %}


What is the template function prototype invoked by Show<10>("abcdefghijklmn")? What's the output?

3. the program's output is not right, please correct the following program with right semantics:



{% highlight C++ %}
template<class T>
T maxEx(T a,T b)
{
 return (a > b) ? a : b;
}

int main()
{
 int nFirst = 10;
 int nSecond = 16;
 cout<<maxEx(nFirst, nSecond)<<endl;            //should be 16

    char *c1 = "a";
    char *c2 = "zoo";
    char *c3 = "ZOO";
    char *c4 = "A";
    cout<<maxEx(c1,c2)<<endl;                       //should be zoo
    cout<<maxEx(c3,c4)<<endl;                       //should be ZOO

 return 0;
}
{% endhighlight %}


4.write the output of the following code.



{% highlight C++ %}
template <class T> void f(T)                    // (d)
{
    cout<<"d"<<endl;
}
template <class T> void f(int, T, double)       // (e)
{
    cout<<"e"<<endl;
}
template <class T> void f(T*)                   // (f)
{
    cout<<"f"<<endl;
}
template <>
void f<double> (double)                         // (g)
{
    cout<<"g"<<endl;
}
void f(double)                                  // (h)
{
    cout<<"h"<<endl;
}

int main()
{
    bool b = true;
    int i = 1;
    double d = 3.14;
    f(b);
    f(i,42,d) ;
    f(&i) ;
    f(d);

 return 0;
}
{% endhighlight %}


5.Case:

{% highlight C++ %}
template <class Type>
class TwoNum
{
private:
    Type a;
    Type b;
public:
    TwoNum(){}
    TwoNum(Type aa , Type bb);

    int Compare(); //比较a 和b的大小

    Type Max() // 求a 和b的最大值
    {
        return (a>b)?a:b;
    }
    Type Min() // 求a 和b的最小值
    {
        return (a>b)?b:a;
    }

    void Setab(Type& aa , Type& bb)
    {
        a=aa; b=bb;
    }

    Type geta()
    {
        return a;
    }

    Type getb()
    {
    return b;
    }
};

template<class Type>
TwoNum<Type>::TwoNum(Type aa ,Type bb)
                   : a(aa), b(bb)
{
    ;
}

template<class Type>
int TwoNum<Type>::Compare()
{
    if(a>b)
        return 1;
    else if(a==b)
        return 0;
    else
        return -1;
}

#include <iostream.h>
void main()
{
    TwoNum<int> x(4,8);
    cout<<x.Compare()<<’ ‘<<x.Max()<<’ ‘<<x.Min()<<endl;

    char ch=’x’;
    TwoNum<char> y(ch,’x’);
    cout<<y.Compare()<<’ ‘<<y.Max()<<’ ‘<<y.Min()<<endl;
}
{% endhighlight %}
Please write the output：

6．Which of the following templates are illegal? Why?

(1)

{% highlight C++ %}
template <class Type>
class Container1;
template <class Type, int size>
class Container1;
{% endhighlight %}

{% highlight C++ %}
template <class Type>
void Container1(Type t);
template <class Type, int size>
void Container1(Type t);
{% endhighlight %}

(2)

{% highlight C++ %}
template <class T,U,class V>
class Container2;
{% endhighlight %}

(3)

{% highlight C++ %}
template<typename myT, class myT>
class Container3;
{% endhighlight %}
(4)

{% highlight C++ %}
template<class Type, int *ptr)
class Container4;
template<class Type, int * pi)
class Container4;
{% endhighlight %}

(5)

{% highlight C++ %}
template <class Type, int val = 0>
class Container6;
{% endhighlight %}

7．correct the class CList declaration (No need to implement the members.)



{% highlight C++ %}
template <class elementType>
class ListItem;

template<class elemType>
class CList
{
public:
    CList(): front(NULL), end(NULL);
    CList (const List &);
    ~CList();

    void insert(ListItem<elemType> *ptr, elemType<elemType> value);
    int remove(elemType<elemType> value);
    size_t size( )
    {
        return _size;
    }
private:
    ListItem<elemType> *front;
    ListItem<elemType> *end;
};
{% endhighlight %}

8.write the output for overload class template



{% highlight C++ %}
template <class T> class mvector                // (a)
{
public:
    void f()
    {
        cout<<"a"<<endl;
    }
};
template <class T> class mvector<T*>            // (b)
{
    T t;
public:
    void f()
    {
        t = 0;
        cout<<"b"<<endl;
    }
};  
template <>   class mvector <void*>             // (c)
{
public:
    void f()
    {
        cout<<"c"<<endl;
    }
};

int main()
{

    mvector<void*>  vpm;
    mvector<int*>   ipm;
    mvector<int>    im;

    vpm.f();
    ipm.f();
    im.f();
}
{% endhighlight %}


ADVANCED:
1．Write a class template CVar<typename> which has following methods:

{% highlight C++ %}
     Operator + (CVar<typename>& )  //plus
     Operator –(CVar<typename>& )  //division
     Operator =(CVar<typename>& )  //assign
     Operator ==(CVar<typename>& )  //equal
     Operator typename()        //cast
     Output();       //output it’s data;
{% endhighlight %}

And other necessary members.

2. Write some global function template:

{% highlight C++ %}
     Operator +( CVar<Typename>& , CVar<Typename>&)
     Operator -( CVar<Typename>& , CVar<Typename>&)
{% endhighlight %}
You can try to comment CVar class operator +/- to test whether your global function is enable.

3. Write a specialized template class CVar<char*> and CVar<bool>.
{% highlight C++ %}
//Note: Using your semantics to implement the algorithm.
// such as :            CVar<char*1> + CVar<char*2> : strcat();
//                          CVar<char*1> - CVar<char*2> : find all char*2 and delete them in char*1.
//                          CVar<bool>   + CVar<bool>   : &
//                          CVar<bool>   - CVar<bool>   : ^
{% endhighlight %}

4. Write a template function my_sort as following:

{% highlight C++ %}
 template<typename Type>
    Void my_sort(Type* array, size_t size);
//NOTE:
//* Maybe you have to implement another 2 function templates:

     template<typename Type>
     bool my_max(Type& lhs, Type& rhs);
     template<typename Type>
     Void my_swap(Type& lhs, Type& rhs);
//* you can decide your concrete sort algorithm.
{% endhighlight %}

EXPLORATION:
1． Design a template queue class and implement the following members:

(1) method void add(Type elem).     //add an element to tail.

(2) method Type remove().           //remove element from head, and return the element.

(3) method Type head().             //return the head value of queue.

(4) method void clear().            //clear all queue.

(5) method bool is_empty().         //indicate whether the queue is empty.

(6) method size_t count().          //return the count.

(7) nested class Iterator to traverse the queue.

(8) method operator+=(Type elem).    //The same to add();

(9) method operator--().             //The same to remove();

(10) method Iterator begin().        //Return the begin of the queue.

(11) method Iterator end().          //Return the end of the queue.

Besides, define an global overload operator:
{% highlight C++ %}
    operator<<;
{% endhighlight %}
to directly output all the values of queue item.

the following is the test of your queue：

{% highlight C++ %}
#include <iostream.h>
#include "queue.h"
using namespace std;

void main()
{
    Queue<int> iq(10);

    for(int i=0; i < 10; i++)
        iq.add(i*5);
    iq--;
    iq += 50;

    if (!iq.is_empty())
        cout << "Removed : " << iq.remove() << " Current Head : " << iq.head();
    cout << endl;
    if (!iq.is_empty())
        cout << iq;
    Queue<int>::Iterator iQueue;
    for(iQueue = iq.begin(); iQueue != iq.end(); iQueue++)
    {
        cout << (*iQueue)<<" ";
    }
    cout << endl;
    iq.clear();
    cout << iq;
}
{% endhighlight %}
The ourput is：
Removed : 5 Current Head : 10
There are 9 queue items: < 10 15 20 25 30 35 40 45 50 >
10 15 20 25 30 35 40 45 50
There are 0 queue items: < >

2.design a class template CHash which algorithm is besed on buckets:
{% highlight C++ %}
template< typename Key, typename Value >
class CHash
{
public:
    class Iterator
    {
    }
    CHash( const size_t nMax,
           ULONG        ( *hashFunc )( const Key tKey ),
           bool         bAutoSize = false );
 CHash( const CHash& hash );
 ~CHash();
 CHash& operator= ( const CHash<Key, Value>& hash );
    operator[];
    Iterator begin();
    Iterator end();
 size_t size();
 void insert( const Key tKey, Value& rValue );
 void clear();
}
{% endhighlight %}

FUN:

1.Write the output of the following code.

{% highlight C++ %}
#include <IOSTREAM>
using std::cout;
using std::endl;

template<int N>
class CalculateCycle
{
public:
    enum { count = CalculateCycle< N % 2 ? (N * 3 + 1) : (N / 2) >::count + 1 };
};

template <>
class CalculateCycle<1>
{
public:
    enum { count = 1 };
};

int main()
{
    const int iNo = 22;
    cout << "Cycle length of " << iNo << " is = "
        << CalculateCycle<iNo>::count << endl;
    return 0;
}
{% endhighlight %}

2.The following is a smart list. Please add other necessary implements to make it work.

{% highlight C++ %}
#include <iostream>

template<typename T>
class CListTemplate
{
public:
    T* left;
    T* right;
    int elem;
};
class CMyList : public CListTemplate<CMyList>
{
public:
    size_t size;
};

template<class T>
class CList : public T
{
public:
 T* Head;
};

int main()
{
    CList<CMyList> my_List;

    //my_List.left->left->right->elem = 10;
 return 0;
}
{% endhighlight %}
