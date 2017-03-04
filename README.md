# AdvancedProgFirstAssignment

#Challenge name: Abstract Classes - Polymorphism
Max Score: 60
In order to get solution I tried to implement a simple LRU cache, at first I actually skipped this task but returned and finished it after completing the STL chapter of C++ chalenges. STL helped me to understand better map class and use of iterator. I've spend a decent ammount of time reading the Node struct and cache class in order to understand the implementation.
p.s. this linked helped to understand the design of LRU cache:
http://stackoverflow.com/questions/2504178/lru-cache-design
#Link to a problem description:
https://www.hackerrank.com/challenges/abstract-classes-polymorphism
#My solution:
//pointer to a base class http://www.cplusplus.com/doc/tutorial/polymorphism/
```
class LRUCache : public Cache{
    private:
    map<int,Node*>::iterator itr; //iterator 
    public:
    //set the capacity
    LRUCache(int capacity){
        cp=capacity;
        head = NULL;
        tail = NULL;
    }
    //set function
    void set(int key, int value){
        if(mp.empty()){   // check if chache is empty
            Node *N;
            N= new Node(key,value);
            tail = head = N;
            mp[key]= N;   
    } else if (mp.size()<cp){ //if there is a space in cache
            mp[key] = new Node(NULL,head, key, value);
            head->prev = mp[key];
            head=mp[key];
        } else { //cache full remove and add data
            Node *N;
            N= tail;
            int lessUsed = tail->key;
            tail= tail->prev;
            mp.erase(lessUsed);
            mp[key]= new Node(NULL, head, key, value);
            head->prev = mp[key];
            head = mp[key];
        }
    }
    
    //get function
    int get(int key){
        itr=mp.find(key);
        if(itr!=mp.end()){
            return mp[key]->value;
        }
      return -1;  
    }
};
```

#Challenge name: Exceptional Server
Max Score: 30
This problem was solved by using exeptions which was a unique expirience because I have never used exeptions before.
#Link to a problem description:
https://www.hackerrank.com/challenges/exceptional-server
#My solution:
//http://www.cplusplus.com/doc/tutorial/exceptions/  
```
		try {
         int result = Server::compute(A, B);
            cout<<result<<endl;
        } catch(bad_alloc& ba){
            cout<<"Not enough memory"<<endl;
        } catch (std::invalid_argument& e){      // if A<0 
            cout<<"Exception: "<<e.what()<<endl;
        } catch (std::exception& e) {
        cout << "Exception: " << e.what() << endl;
        } catch(...){               //http://stackoverflow.com/questions/315948/c-catching-all-exceptions
            cout<<"Other Exception"<<endl;
        }
	```
       
#Challenge name: Magic Spells
Max Score: 40
This was a challenge I stucked for a couple of days. Thanks to Abdullah who said that it is a longest common subsequence problem not only a dynamic cast one. 
p.s link that helped to understand the lcs
http://www.geeksforgeeks.org/dynamic-programming-set-4-longest-common-subsequence/
#Link to a problem description: 
https://www.hackerrank.com/challenges/magic-spells
#My solution:
```
//first part is a dynamic cast conversion that goes through all spell classes
Fireball* fball = dynamic_cast<Fireball*>(spell);
if(fball!=NULL){
        fball->revealFirepower();
        return;
}

Frostbite* fbite = dynamic_cast<Frostbite*>(spell);
if (fbite != NULL) {
    fbite->revealFrostpower();
    return;
}

Thunderstorm* tstorm = dynamic_cast<Thunderstorm*>(spell);
if (tstorm != NULL) {
    tstorm->revealThunderpower();
    return;
}

Waterbolt* wtbolt = dynamic_cast<Waterbolt*>(spell);
if (wtbolt != NULL) {
    wtbolt->revealWaterpower();
    return;
}
   
// this part is LCS problem solution 

    string scroll = spell->revealScrollName(); //geting access to strings
    string  sj = SpellJournal::journal;

    int m = sj.length()+1; //another variables to reduce the code size
    int n = scroll.length()+1;
   
    vector < vector<int> > longest(m, vector<int>(n)); //i've tried to use two dimentional arrays at first it didnt pass all test cases 
    for(int i = 1;i<m; i++ ){
        for(int j=1; j<n; j++){
            if(scroll[j-1]==sj[i-1]){
                longest[i][j]= longest[i-1][j-1]+1;
            }else{
                if(longest[i][j-1]>longest[i-1][j]){
                    longest[i][j]= longest[i][j-1];
                } else{
                    longest[i][j]= longest[i-1][j];
                }
            }
        }
    }

   cout<<longest[m-1][n-1]<<endl; 
   ```
   
#Challenge name: Virtual Functions
Max score: 40
Link that helped:
http://www.cplusplus.com/doc/tutorial/polymorphism/
#Link to problem description:
https://www.hackerrank.com/challenges/virtual-functions
#My solution:
```
class Person{
    public:
    string name;
    int age;
    
    virtual void getdata() = 0;
    virtual void putdata() = 0;
};
    int prof_id = 0;
    int stud_id = 0;


class Professor : public Person{
    public:
    int pub;
    int id1;
    
    Professor(){
        ++prof_id;
    }
    
    void getdata(){
        cin>>name;
        cin>>age;
        cin>>pub;  
        id1 = prof_id;
    }
    void putdata(){
        cout<<name<<" ";
        cout<<age<<" ";
        cout<<pub<<" ";
        
        cout<<id1<<endl; 
    }
    
};
class Student : public Person{
    public:
    int marks[6];
    int sum = 0;
    int id2;
    Student(){
        ++stud_id;
    }
    
    void getdata(){
        cin>>name;
        cin>>age;
        for(int i = 0; i<6; i++){
            cin>>marks[i];
        }
        id2=stud_id;
    }
    
    void putdata(){
        cout<<name<<" ";
        cout<<age<<" ";
        for(int j = 0; j<6; j++){
            sum+= marks[j];
        }
        cout<<sum<<" ";
        
        cout<<id2<<endl;
        
    }
    
};
```
#Challenge name: 
