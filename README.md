Download Link: https://assignmentchef.com/product/solved-cop4530-project5-hash-tables-and-its-applications
<br>
Understand and get familiar with the hash table data structure, along with its application in managing user accounts.

<strong>Task:</strong> Implement a hash table ADT and other supporting user interfaces;  develop a simple password server program.

<strong>Project Description: </strong>

This project contains two parts. In the first part of the project, you need to implement a hash table class template named HashTable. In the second part of the project, you will develop a simple password server program using the hash table you developed.

<strong>Task 1: Requirements of HashTable Class Template</strong>

<ul>

 <li>Your implementation of HashTable must be in the namespace of cop4530.</li>

 <li>You must provide the template declaration and implementation in two different files hashtable.h (containing HashTable class template declaration) and hashtable.hpp (containing the implementation of member functions). You must include hashtable.hpp inside hashtable.h as we have done in the previous projects. The two files hashtable.h and hashtable.hpp will be provided to you, which contain some helpful functions that you will need to use in developing the hash table class template.</li>

 <li>You must implement hash table using the technique of chaining with separate lists (separate chaining). That is, the internal data structure of the hash table class template should be a vector of lists. Use the STL containers for the internal storage (instead of any containers you developed in the previous projects).</li>

 <li>You must at least implement all the interfaces specified below for the HashTable class template.</li>

</ul>




<strong>Public HashTable interface</strong> (K and V are template parameters (generic data types), which represent the key and value types for a table entry, respectively)

<ul>

 <li><strong>HashTable(size_t size = 101)</strong>: constructor. Create a hash table, where the size of the vector is set to prime_below(size) (where size is default  to 101), where prime_below() is a private member function of the HashTable and provided to you.</li>

 <li><strong>~HashTable()</strong>: destructor. Delete all elements in hash table.</li>

 <li><strong>bool contains(const K &amp; k)</strong>: check if key k is in the hash table.</li>

 <li><strong>bool match(const std::pair&lt;K, V&gt; &amp;kv) </strong>: check if key-value pair is in the hash table.</li>

 <li><strong>bool insert(const std::pair&lt;K, V&gt; &amp; kv):</strong> add  the key-value pair kv into the hash table. Don’t add if kv is already in the hash table. If the key is the hash table but with a different value, the value should be updated to the new one with kv. Return true if kv is inserted or the value is updated; return false otherwise (i.e., if kv is in the hash table).</li>

 <li><strong>bool insert (std::pair&lt;K,  V&gt; &amp;&amp; kv)</strong>: move version of insert.</li>

 <li><strong>bool remove(const K &amp; k)</strong>: delete the key k and the corresponding value if it is in the hash table. Return true if k is deleted, return false otherwise (i.e., if key k is not in the hash table).</li>

 <li><strong>void clear()</strong>: delete all elements in the hash table</li>

 <li><strong>bool load(const char *filename)</strong>: load the content of the file with name filename into the hash table. In the file, each line contains a single pair of key and value, separated by a white space.</li>

 <li><strong>void dump()</strong>: display all entries in the hash table. If an entry contains multiple key-value pairs, separate them by a semicolon character (:) (see the provided executable for the exact output format).</li>

 <li><strong>size_t size()</strong>: return the size of the hash table (i.e. number of entries stored).</li>

 <li><strong>bool write_to_file(const char *filename)</strong>: write all elements in the hash table into a file with name filename. Similar to the file format in the load function, each line contains a pair of key-value pair, separated by a white space.</li>

</ul>

<strong>Private helper functions</strong>

<ul>

 <li><strong>void makeEmpty()</strong>: delete all elements in the hash table. The public interface clear() will call this function.</li>

 <li><strong>void rehash()</strong>: Rehash function. Called when the number of elements in the hash table is greater than the size of the vector.</li>

 <li><strong>size_t myhash(const K &amp;k)</strong>: return the index of the vector entry where k should be stored.</li>

 <li><strong>unsigned long prime_below (unsigned long)</strong> and <strong>void setPrimes(vector&lt;unsigned long&gt;&amp;)</strong>: two helpful functions to determine the proper prime numbers used in setting up the vector size. Whenever you need to set hash table to a new size “sz”, call prime_below(sz) to determine the new proper underlying vector size. These two functions have been provided in hashtable.h and hashtable.hpp.</li>

</ul>

Make sure to declare as const member functions any for which this is appropriate

You need to write a simple test program to test various functions of hash table. More details are provided in a later part of this description.




<strong>Task 2: Requirements of the Password Server Class (PassServer)</strong>

<ul>

 <li>Name the password server class as PassServer. Its declaration and implementation should be provided in two files, passserver.h and passserver.cpp, respectively.</li>

 <li>PassServer should be implemented as an adaptor class, with the HashTable you developed as the adaptee class. The type for both K and V in HashTable should be string. The key and value will be the username and password, respectively.</li>

 <li>PassServer must store username and <em>encrypted</em> password pairs in the hash table.</li>

 <li>PassServer must at least support the following member functions (again, make sure to declare as <em>const</em> member functions any that are appropriate):</li>

</ul>

<strong>Public interface:</strong>

<ul>

 <li style="list-style-type: none;">

  <ol>

   <li><strong>PassServer(size_t size = 101)</strong>: constructor, create a hash table of the specified size. You just need to pass this size parameter to the constructor of the HashTable. Therefore, the real hash table size could be different from the parameter size (because prime_below() will be called in the constructor of the HashTable).</li>

   <li><strong>~PassServer()</strong>: destructor. You need to decide what you should do based on your design of PassServer (how you develop the adaptor class based on the adaptee HashTable). In essence, we do not want to have memory leak.</li>

   <li><strong>bool load(const char *filename)</strong>: load a password file into the HashTable object. Each line contains a pair of username and encrypted password.</li>

   <li><strong>bool addUser(std::pair&lt;string,  string&gt; &amp; kv): </strong>add a new username and password.  The password passed in is in plaintext, it should be encrypted before insertion.</li>

   <li><strong>bool addUser(std::pair&lt;string, string&gt; &amp;&amp; kv): </strong>move version of addUser.</li>

   <li><strong>bool removeUser(const string &amp; k)</strong>: delete an existing user with username k.</li>

   <li><strong>bool changePassword(const std::pair&lt;string, string&gt; &amp;p, const string &amp; newpassword)</strong>: change an existing user’s password. Note that both passwords passed in are in plaintext. They should be encrypted before you interact with the hash table. If the user is not in the hash table, return false. If p.second does not match the current password, return false. Also return false if the new password and the old password are the same (i.e., we cannot update the password).</li>

   <li><strong>bool find(const string &amp; user):</strong> check if a user exists (if user is in the hash table).</li>

   <li><strong>void dump()</strong>: show the structure and contents of the HashTable object to the screen. Same format as the dump() function in the HashTable class template.</li>

   <li><strong>size_t size():</strong> return the size of the HashTable (the number of username/password pairs in the table).</li>

   <li><strong>bool write_to_file(const char *filename):</strong> save the username and password combination into a file. Same format as the write_to_file() function in the HashTable class template.</li>

  </ol></li>

</ul>

<strong>Private helper function:</strong>

<ul>

 <li style="list-style-type: none;">

  <ul>

   <li><strong>string encrypt(const string &amp; str)</strong>: encrypt the parameter str and return the encrypted string.</li>

  </ul></li>

</ul>

For this project, we shall use the GNU C Library’s <strong>crypt()</strong> method to encrypt the password.  The algorithm for the crypt() method shall be MD5-based.  The <em>salt</em> shall be the character stream “$1$########”.   The resulting encrypted character stream is the

“$1$########” + �$’ + 22 characters = 34 characters in total.

A user password is the sub string containing the last 22 characters, located after the 3<sup>rd</sup> �$’.

<strong>Note:</strong> A sample program to demonstrate the use of the <strong>crypt()</strong> method is also provided. In order compile a program calling crypt(), you will need to link with the crypt library when you compile. You can read more information on the manual page of crypt(). Example compile command (used to build the sample scrypt.x program):

g++ -std=c++11 scrypt.cpp -lcrypt -o scrypt.x




<strong>Driver Program</strong>: In addition to developing the HashTable class template and the PassServer class, you need to write a driver program to test your code. Name the driver program proj5.cpp.

<ul>

 <li>A partial implementation of proj5.cpp is provided to you, which contains a Menu() function. You must use this function as the standard option menu for user to type input.  You may not alter the Menu function.</li>

 <li>The driver program must re-prompt the user for the next choice from the menu and exit the program only when the user selection the exit “x” option.</li>

 <li>Run the provided executable x on linprog to see the expected behavior of each of the menu options, and the expected order of inputs. Make sure to test with error cases too, so that you see the appropriate error messages that are printed</li>

</ul>




<strong>Extra-credit (10 points)</strong>

You may submit an alternative version to your program named sproj5.cpp, in which the program hides the user’s entries whenever the user keys in a password or new password.

<ul>

 <li>Do not use the getpass() function, which is obsolete.</li>

</ul>




<h2>Provided Partial Code</h2>

The following <a href="https://www.cs.fsu.edu/~myers/cop4530/hw/hw5files/proj5_provided.tar">partial code</a> has been provided to you.

<ol>

 <li>hashtable.h: partial implementation</li>

 <li>hashtable.hpp: partial implementation</li>

 <li>proj5.cpp: driver program, partial implementation.</li>

 <li>proj5.x : sample executable for linprog.cs.fsu.edu</li>

 <li>sproj5.x: sample executable with hidden password entries for linprog.cs.fsu.edu</li>

 <li>test1: sample test case (which contains the commands that a user will type). You can redirect it to proj5.x as “proj5.x &lt; test1”. Results will save in the file “outtest1”</li>

 <li>scrypt.cpp: sample program to use crypt() to encrypt password.<strong> </strong></li>

 <li>scrypt.x: executable code of scrypt.cpp.</li>

</ol>


