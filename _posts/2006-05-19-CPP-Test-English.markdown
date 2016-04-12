---
layout: blogs_item
title: C++ STL 习题
author: AcePeak
categories:
  - 积累
tags:
  - C++
  - STL
  - 试题
  - 原创
---

#Questions:

##BASE:

1. which are wrong?

{% highlight C++ %}
int ia[ 7 ] = { 0, 1, 1, 2, 3, 5, 8 };
(a) vector< vector< int > > ivec;
(b) vector< int > ivec = { 0, 1, 1, 2, 3, 5, 8 };
(c) vector< int > ivec( ia, ia+7 );
(d) vector< string > svec = ivec;
(e) vector< string > svec( 10, string( "null" ));
{% endhighlight %}


2. Change code style to STL and compare their efficiency.

{% highlight C++ %}
// ***** C-style character string implementation *****
int main()
{
    int errors = 0;
    const char *pc = "a very long literal string";
    for ( int ix = 0; ix < 1000000; ++ix )
    {
        int len = strlen( pc );
        char *pc2 = new char[ len + 1 ];
        strcpy( pc2, pc );
        if ( strcmp( pc2, pc ))
            ++errors;
        delete [] pc2;
    }
    cout << "C-style character strings: " << errors << " errors occurred.\n";
}
{% endhighlight %}


3.accept some ints from standard input, then sort them and output to standard output. Please use STL as far as possible.


##ADVANCED:

1.What are the types of std::cin and std::cout? Write a console program ECHO that can be invoked by the following ways:

{% highlight ruby %}
    ECHO [infile] [outfile]                             //[] indicates the infile is not necessary.
                                                        //there must be one and only one between -i and -s.
The test case are :

    ECHO infile.txt outfile.txt                         //read from infile.txt and write to outfile.txt.
    ECHO infile.txt                                     //read from infile.txt and write to screen.
    ECHO                                                //read from standard input and write to standard output.

//related:ofstream, ifstream, ostream, istream.
{% endhighlight %}

2.Try your best to write a class to implement two-dimensional arrays like built-in type.

{% highlight C++ %}
    int a[10][10];
    a[0][0] = 5;

    YourClass<int> yc(10,10);
    yc[0][0] = 5;
{% endhighlight %}


3.write a program to process students' scores table(by using map/multimap).
    a.student infomation is like this:
            name, C++ basic score, C++ OOP score, C++ template score, C++ STL score, C++ MFC score
    b.sort by name.
    d.traverse infotable and generate the total score and average score to another table.
    e.output name, total score, average score and place for each student sorting by place.


4. write a program to read words and calculate every word's frequency from a file. Output the 20 words and frequency with most high frequency.

{% highlight C++ %}
//
//Note:
//token - a set of characters bound on either side by spaces, the beginning of
//the input string parameter or the end of the input String parameter.
//word - a token that contains only letters (a-z or A-Z) and may end with a
//single period or a single comma. A word must have at least one letter.
//
//  this is a word.
//          //token(4) : this is a word.
//          //words(4) : this is a word
{% endhighlight %}


##EXPLORATION:

1. How and when is std::auto_ptr used? can std::auto_ptr be put on argument list? why?


2. Compare vector with deque. When do we use each?


3. What does the following code do? write a better method.

{% highlight C++ %}
    vector<Type> c( 10000 );
    c.erase( c.begin() + 10, c.end() );
    c.reserve( 10 );
{% endhighlight %}


4.what does the std::remove() algorithm do? Does the algorithm remove what should be removed really? What's the difference in size and capacity between before and after? Write the right remove method.

5.write a file_iterator，and 3 functors，to make the following code work：

{% highlight C++ %}
int main()
{
  // count of file entries in the directory
  cout << "Total count: "
       << count_if(file_iterator(), file_iterator(0),
                   always_true<file_iterator::value_type>())
       << endl;

  // for_each() to display all entries
  for_each(file_iterator(), file_iterator(0), display_file_entry());

  // accumulate() to add up the size of all file entries
  cout << "Total: ";
  cout << accumulate(file_iterator(), file_iterator(0), 0,
                     file_size())
       << "bytes." << endl;

  return 0;
}
{% endhighlight %}

the test case(the program name is mydir)：

{% highlight ruby %}
c:\> mydir
Total count: 3
...(filename)
...(filename)
...(filename)
Total: 102487 bytes.
{% endhighlight %}


##FUN:

1.you want to write a class template C that can be instantiated only on types that have a member function named Clone() that takes no parameters and returns a pointer to the same kind of object.

{% highlight C++ %}
//T must provide T* T::Clone() const
template<typename T>
class C
{
  //
}
{% endhighlight %}

> Note: It's obvious that if C writes code that just tries to invoke T::Clone() without parameters, then such code will fail to compile if there isn't a T::Clone() that can be called without parameters.

2.try the following code in VC6 and VC.net 2003 seperately:



{% highlight C++ %}
#include <iostream>
#include <string>
using namespace std;
int main()
{
    string str1("Hello, World!");
    string str2(str1);
    char* c = const_cast<char*> (str1.c_str()) ;
    *c = 'h';
    cout<<str1<<endl;
    cout<<str2<<endl;
}
{% endhighlight %}

Why are the results different?
