Download Link: https://assignmentchef.com/product/solved-cs30-project-1-the-year-of-the-quarantine
<br>
<strong><em><u>Project 1:  The Year of the Quarantine</u></em></strong>

Apparently, 2020 didn’t get the memo.  Every year, we like to celebrate milestones.  That might be a graduation, whether it’s kindergarten, high school, or college.  There were supposed to be weddings, whether here or at a destination.  Most importantly, I was supposed to celebrate my 40<sup>th</sup> birthday during the summer.  Big blowout, big barbecue, friends getting back together, enjoying memories, great food, and maybe one (or more) adult beverages.  Alas, 2020 isn’t having any of that.  In fact, every celebration is pretty much being sponsored by Zoom, Google Meet, or WebEx.  In other words, it’s the Year of the Quarantine.  Nevertheless, I’m going to celebrate…and you’ll be celebrating with me.  I’m still going to have a big guest list, just virtually.

To help me out, you will write the implementation of the BirthdayParty using a doubly linked list, which should be sorted alphabetically according to last name, then first name. You will also implement a couple of algorithms that operate on a BirthdayParty.  <strong><u>Implement BirthdayParty</u> </strong>

Consider the following BirthdayParty interface:

typedef std::string BirthdayType;

class BirthdayParty

{   public:

BirthdayParty();       // Create an empty BirthdayParty list

bool noInvitees() const;  // Return true if the BirthdayParty list                                 // is empty, otherwise false.

int whosOnTheGuestList() const;  // Return the number of players in

// the BirthdayParty list.

bool addInvitee(const std::string&amp; firstName, const std::string&amp;                 lastName, const BirthdayType&amp; value);

// If the full name (both the first and last name) is not equal

// to any full name currently in the list then add it and return

// true. Elements should be added according to their last name.

// Elements with the same last name should be added according to

// their first names. Otherwise, make no change to the list and       // return false (indicating that the name is already in the        // list).

bool modifyInvitee(const std::string&amp; firstName, const std::string&amp; lastName, const BirthdayType&amp; value);

// If the full name is equal to a full name currently in the

// list, then make that full name no longer map to the value it        // currently maps to, but instead map to the value of the third        // parameter; return true in this case. Otherwise, make no        // change to the list and return false.

bool addOrModify(const std::string&amp; firstName, const std::string&amp; lastName, const BirthdayType&amp; value);

// If full name is equal to a name currently in the list, then

// make that full name no longer map to the value it currently

// maps to, but instead map to the value of the third parameter;

// return true in this case. If the full name is not equal to

// any full name currently in the list then add it and return        // true. In fact, this function always returns true.

bool dropFromGuestList(const std::string&amp; firstName, const std::string&amp; lastName);

// If the full name is equal to a full name currently in the

// list, remove the full name and value from the list and return        // true.  Otherwise, make no change to the list and return        // false.

bool personOnGuestList(const std::string&amp; firstName, const std::string&amp; lastName) const;

// Return true if the full name is equal to a full name        // currently in the list, otherwise false.

bool checkGuestList(const std::string&amp; firstName, const std::string&amp; lastName, BirthdayType&amp; value) const;

// If the full name is equal to a full name currently in the

// list, set value to the value in the list that that full name        // maps to, and return true.  Otherwise, make no change to the        // value parameter of this function and return false.

bool selectInvitee(int i, std::string&amp; firstName, std::string&amp; lastName, BirthdayType&amp; value) const;

// If 0 &lt;= i &lt; size(), copy into firstName, lastName and value

// parameters the corresponding information of the element at

// position i in the list and return true.  Otherwise, leave the

// parameters unchanged and return false. (See below for details

// about this function.)




void changeGuestList(BirthdayParty&amp; other);

// Exchange the contents of this list with the other one. };




The addInvitee function primarily places elements so that they are sorted in the list based on last name. If there are multiple entries with the same last name then those elements, with the same last name, are added so that they are sorted by their first name. In other words, this code fragment

BirthdayParty theLastDance;




theLastDance.addInvitee (“Michael”, “Jordan”, 23);     theLastDance.addInvitee (“Scottie”, “Pippen”, 33);     theLastDance.addInvitee (“Dennis”, “Rodman”, 91);     theLastDance.addInvitee (“Luc”, “Longley”, 13);     theLastDance.addInvitee (“Ron”, “Harper”, 9);

for (int n = 0; n &lt; theLastDance.whosOnTheGuestList(); n++)

{         string first;         string last;         int val;         theLastDance.selectInvitee (n, first, last, val);         cout &lt;&lt; first &lt;&lt; ” ” &lt;&lt; last &lt;&lt; ” ” &lt;&lt; val &lt;&lt; endl;

}




must result in the output:

Ron Harper 9

Michael Jordan 23     Luc Longley 13

Scottie Pippen 33

Dennis Rodman 91




Notice that the empty string is just as good a string as any other; you should not treat it in any special way:

BirthdayParty dodgers;     dodgers.addInvitee(“Clayton”, “Kershaw”, 31.0);     dodgers.addInvitee(“Cody”, “Bellinger”, 11.5);     assert(!dodgers.personOnGuestList (“”,””));     dodgers.addInvitee(“Mookie”, “Betts”, 27.0);     dodgers.addInvitee(“”, “”, 0.57);     dodgers.addInvitee(“Justin”, “Turner”, 20.0);     assert(dodgers.personOnGuestList (“”, “”));     dodgers.dropFromGuestList(“Mookie”, “Betts”);     assert(dodgers.whosOnTheGuestList() == 4

&amp;&amp; dodgers.personOnGuestList(“Clayton”, “Kershaw”)

&amp;&amp; dodgers.personOnGuestList (“Cody”, “Bellinger”)

&amp;&amp; dodgers.personOnGuestList (“Justin”, “Turner”)

&amp;&amp; dodgers.personOnGuestList (“”, “”));

When comparing keys for addInvitee, modifyInvitee, addOrModify, dropFromGuestList, personOnGuestList, and checkGuestList, just use the == or != operators provided for the string type by the library. These do case-sensitive comparisons, and that’s fine.

For this project, implement this BirthdayParty interface using a doubly-linked list. (You must not use any container from the C++ library.)

For your implementation, if you let the compiler write the destructor, copy constructor, and assignment operator, they will do the wrong thing, so you will have to declare and implement these public member functions as well:

<strong><em>Destructor </em></strong>

When a BirthdayParty is destroyed, all dynamic memory must be deallocated.

<h1><em>Copy Constructor </em></h1>

When a brand new BirthdayParty is created as a copy of an existing BirthdayParty, a deep copy should be made.

<h1><em>Assignment Operator </em></h1>

When an existing BirthdayParty (the left-hand side) is assigned the value of another BirthdayParty (the right-hand side), the result must be that the left-hand side object is a duplicate of the right-hand side object, with no memory leak (i.e. no memory from the old value of the left-hand side should be still allocated yet inaccessible).

Notice that there is no a priori limit on the maximum number of elements in the

BirthdayParty (so addOrModify should always return true). Also, if a BirthdayParty has a size of n, then the values of the first parameter to the selectInvitee member function are 0, 1, 2, …, n – 1; for other values, it returns false without setting its parameters.

<h1>Implement Some Non-Member Functions</h1>

Using only the <em>public</em> interface of BirthdayParty, implement the following two functions. (Notice that they are non-member functions; they are not members of BirthdayParty or any other class.)

bool combineGuestLists(const BirthdayParty &amp; bpOne,                  const BirthdayParty &amp; bpTwo,

BirthdayParty &amp; bpJoined);




When this function returns, bpJoined must consist of pairs determined by these rules:

If a full name appears in exactly one of bpOne and bpTwo, then bpJoined must contain an element consisting of that full name and its corresponding value.

If a full name appears in both bpOne and bpTwo, with the same corresponding value in both, then bpJoined must contain an element with that full name and value.

When this function returns, bpJoined must contain no elements other than those required by these rules. (You must not assume bpJoined is empty when it is passed in to this function; it might not be.)

If there exists a full name that appears in both bpOne and bpTwo, but with different corresponding values, then this function returns false; if there is no full name like this, the function returns true. Even if the function returns false, result must be constituted as defined by the above rules.

For example, suppose a BirthdayParty maps the full name to integers. If bpOne consists of these three elements

“Kobe” “Bryant” 8   “AC” “Green” 45 “Shaquille” “Oneal” 34    and bpTwo consists of

“Kobe” “Bryant” 8 “Horace” “Grant” 54

then no matter what value it had before, bpJoined must end up as a list consisting of

“Kobe” “Bryant” 8 “Horace” “Grant” 54 “AC” “Green” 45

“Shaquille” “Oneal” 34

and combineGuestLists must return true.

If instead, bpOne consists of

“Kobe” “Bryant” 8   “AC” “Green” 45 “Shaquille” “Oneal” 34 and bpTwo consists of

“Kobe” “Bryant” 24 “Pau” “Gasol” 16

then no matter what value it had before, bpJoined must end up as a list consisting of

“Pau” “Gasol” 16 “AC” “Green” 45 “Shaquille” “Oneal” 34




and combineGuestLists must return false.

void verifyGuestList (const std::string&amp; fsearch,                   const std::string&amp; lsearch,                    const BirthdayParty&amp; bpOne,

BirthdayParty&amp; bpResult);




When this function returns, bpResult must contain a copy of all the elements in bpOne that match the search terms; it must not contain any other elements. You can wildcard the first name, last name or both by supplying “*”. (You must not assume result is empty when it is passed in to this function; it may not be.)

For example, if memories consists of the three elements

“Gianna” “Bryant” 13   “Kobe” “Bryant” 41   “Little” “Richard”

87   “Jerry” “Stiller” 92  and the following call is made:

verifyGuestList(“*”, “Bryant”, memories, bpResult);

then no matter what value it had before, bpResult must end up as a BirthdayParty consisting of

“Gianna” “Bryant” 13   “Kobe” “Bryant” 41

If instead, moreMemories were

“Kirk” “Douglas” 103   “Fred” “Neal” 77   “Pop” “Smoke” 20

“Fred” “Willard” 86

and the following call is made:

verifyGuestList(“Fred”, “*”, moreMemories, result);

then no matter what value it had before, result must end up as a list consisting of

“Fred” “Neal” 77   “Fred” “Willard” 86

If the following call is made:

verifyGuestList(“*”, “*”, memories, result);

then no matter what value it had before, result must end up being a copy of memories.

Be sure these functions behave correctly in the face of aliasing: What if moreMemories and result refer to the same BirthdayParty, for example?

<h1>Other Requirements</h1>

Regardless of how much work you put into the assignment, your program will receive a low score for correctness if you violate these requirements:

<ul>

 <li>Your class definition, declarations for the two required non-member functions, and the implementations of any functions you choose to inline must be in a file named h, which must have appropriate include guards. The implementations of the functions you declared in BirthdayParty.h that you did not inline must be in a file named BirthdayParty.cpp. Neither of those files may have a main routine (unless it’s commented out). You may use a separate file for the main routine to test your BirthdayParty class; you won’t turn in that separate file.</li>

 <li>Except to add a destructor, copy constructor, assignment operator, and dump function (described below), you must not add functions to, delete functions from, or change the public interface of the BirthdayParty You must not declare any additional struct/class outside the BirthdayParty class, and you must not declare any public struct/class inside the BirthdayParty class. You may add whatever private data members and private member functions you like, and you may declare private structs/classes inside the BirthdayParty class if you like. The source files you submit for this project must not contain the word friend. You must not use any global variables whose values may be changed during execution.</li>

 <li>If you wish, you may add a public member function with the signature void dump() const. The intent of this function is that for your own testing purposes, you can call it to print information about the map; we will never call it. You do not have to add this function if you don’t want to, but if you do add it, it must not make any changes to the map; if we were to replace your implementation of this function with one that simply returned immediately, your code must still work correctly. The dump function must not write to cout, but it’s allowed to write to cerr.</li>

 <li>Your code must build successfully (either Xcode or Visual C++) if linked with a file that contains a main routine, but it must also use standard C++.</li>

 <li>You must have an implementation for every member function of</li>

</ul>

BirthdayParty, as well as the non-member functions combineGuestLists and verifyGuestList. Even if you can’t get a function implemented correctly, it must have an implementation that at least builds successfully. For example, if you don’t have time to correctly implement

BirthdayParty::dropFromGuestList or verifyGuestList, say, here

are implementations that meet this requirement in that they at least build successfully:

bool BirthdayParty::dropFromGuestList(const std::string&amp; fname,                         const std::string&amp; lname)

{    return false; // not correct, but at least this code compiles

}

void verifyGuestList(const std::string&amp; fsearch, const std::string&amp;     lsearch, const BirthdayParty&amp; bpOne, BirthdayParty&amp; bpResult)

{    return; // not correct, but at least this code compiles }




You’ve probably met this requirement if the following file compiles and links with your code. (This uses magic beyond the scope of CS 30.)

#include “BirthdayParty.h”

#include &lt;type_traits&gt;




#define CHECKTYPE(f, t) { auto p = (t)(f); (void)p; }

static_assert(std::is_default_constructible&lt;BirthdayParty&gt;::valu e,

“Map must be default-constructible.”);

static_assert(std::is_copy_constructible&lt;BirthdayParty&gt;::value,

“Map must be copy-constructible.”);

void ThisFunctionWillNeverBeCalled()

{

CHECKTYPE(&amp;BirthdayParty::operator=, BirthdayParty&amp;

(BirthdayParty::*)(const BirthdayParty&amp;));

CHECKTYPE(&amp;BirthdayParty::noInvitees, bool

(BirthdayParty::*)() const);

CHECKTYPE(&amp;BirthdayParty::whosOnTheGuestList, int

(BirthdayParty::*)() const);

CHECKTYPE(&amp;BirthdayParty::addInvitee, bool (BirthdayParty::*)

(const std::string&amp;, const std::string&amp;, const

BirthdayType&amp;));

CHECKTYPE(&amp;BirthdayParty::modifyInvitee, bool

(BirthdayParty::*)(const std::string&amp;, const std::string&amp;,         const BirthdayType&amp;));

CHECKTYPE(&amp;BirthdayParty::addOrModify, bool

(BirthdayParty::*)(const std::string&amp;, const std::string&amp;,         const BirthdayType&amp;));

CHECKTYPE(&amp;BirthdayParty::dropFromGuestList, bool

(BirthdayParty::*)

(const std::string&amp;, const std::string&amp;));

CHECKTYPE(&amp;BirthdayParty::personOnGuestList, bool

(BirthdayParty::*)(const std::string&amp;, const std::string&amp;)         const);

CHECKTYPE(&amp;BirthdayParty::checkGuestList, bool

(BirthdayParty::*)

(const std::string&amp;, const std::string&amp;, BirthdayType&amp;) const);

CHECKTYPE(&amp;BirthdayParty::selectInvitee, bool

(BirthdayParty::*)

(int, std::string&amp;, std::string&amp;, BirthdayType&amp;)         const);

CHECKTYPE(&amp;BirthdayParty::changeGuestList, void

(BirthdayParty::*)(BirthdayParty&amp;));




CHECKTYPE(combineGuestLists,  bool (*)(const BirthdayParty&amp;, const

BirthdayParty&amp;, BirthdayParty&amp;));

CHECKTYPE(verifyGuestList, void (*)(const std::string&amp;,      const std::string&amp;, const BirthdayParty&amp;, BirthdayParty&amp;));

}

int main()

{}




If you add #include &lt;string&gt; to BirthdayParty.h, have the typedef define

BirthdayType as std::string, and link your code to a file containing

#include “BirthdayParty.h”

#include &lt;string&gt;

#include &lt;iostream&gt; #include &lt;cassert&gt; using namespace std;




void test()

{

BirthdayParty aListCommissioners;

assert(aListCommissioners.addInvitee(“Adam”, “Silver”,

“<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="a4c5d7cdc8d2c1d6e4cac6c58ac7cbc9">[email protected]</a>”));    assert(aListCommissioners.addInvitee(“Roger”, “Goodell”,

“<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="473520282823222b2b0729212b6924282a">[email protected]</a>”));    assert(aListCommissioners.whosOnTheGuestList() == 2);

string first, last, e;

assert(aListCommissioners.selectInvitee(0, first, last, e)

&amp;&amp; e == “<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="88faefe7e7ecede4e4c8e6eee4a6ebe7e5">[email protected]</a>”);    assert(aListCommissioners.selectInvitee(1, first, last, e)

&amp;&amp; (first == “Adam” &amp;&amp; e == “<a href="/cdn-cgi/l/email-protection" class="__cf_email__" data-cfemail="b3d2c0dadfc5d6c1f3ddd1d29dd0dcde">[email protected]</a>”));

return; }

int main() {    test();    cout &lt;&lt; “Passed all tests” &lt;&lt; endl;    return 0;

}




the linking must succeed. When the resulting executable is run, it must write Passed all tests to cout and nothing else to cout.

If we successfully do the above, then make no changes to BirthdayParty.h other than to change the typedefs for BirthdayParty so that BirthdayType specifies int, recompile BirthdayParty.cpp, and link it to a file containing

#include ” BirthdayParty.h”

#include &lt;string&gt;

#include &lt;iostream&gt; #include &lt;cassert&gt; using namespace std;




void test()

{

BirthdayParty terribleCommissioners;

assert(terribleCommissioners.addInvitee(“Gary”, “Bettman”,

68));    assert(terribleCommissioners.addInvitee(“Robert”, “Manfred”,

61));    assert(terribleCommissioners.whosOnTheGuestList() == 2);

string first, last;    int a;     assert(terribleCommissioners.selectInvitee(0, first, last, a)

&amp;&amp; a == 68);    assert(terribleCommissioners.selectInvitee(1, first, last, a)

&amp;&amp; (first == “Robert” &amp;&amp; a == 61));

return;

}  int main() {    test();    cout &lt;&lt; “Passed all tests” &lt;&lt; endl;    return 0;

}




the linking must succeed. When the resulting executable is run, it must write Passed all tests to cout and nothing else to cout.

During execution, if a client performs actions whose behavior is defined by this spec, your program must not perform any undefined actions, such as dereferencing a null or uninitialized pointer.

Your code in BirthdayParty.h and BirthdayParty.cpp must not read anything from cin and must not write anything whatsoever to cout. If you want to print things out for debugging purposes, write to cerr instead of cout. cerr is the standard error destination; items written to it by default go to the screen. When we test your program, we will cause everything written to cerr to be discarded instead — we will never see that output, so you may leave those debugging output statements in your program if you wish.