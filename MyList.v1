#include<iostream>
using namespace std;
template<class T> class MyList;
template<class T> MyList<T> operator+(const MyList<T> &l1, const MyList<T> &l2); 
template<class T> MyList<T> operator+(const MyList<T> &l1, const T &item);
template<class T> ostream &operator<<(ostream &os, const MyList<T> &obj);

template<class T> void quicksort(T a[], int low, int high);
template<class T> int divide(T a[], int low, int high);
template<class T> void inverse(T a[], int n);

template<class T>
class MyList{
	friend MyList operator+ <>(const MyList<T> &l1, const MyList<T> &l2); 
	friend MyList operator+ <>(const MyList<T> &l1, const T &item);
	friend ostream &operator<< <>(ostream &os, const MyList<T> &obj);
private:
	int size;
	int len;
	T *a;
	void double_space();
public:
	MyList(){size=100; len=0; a=new T [size];}
	MyList(const MyList &l);
	MyList(int num, const T &item);
	MyList(const MyList &l, int n);
	void push(const T &item);
	T pop();
	void insert(int index, const T &item);
	void clean();
	int get_size();
	void erase(int start, int end);
	T get_item(int index);
	MyList get_item(int start, int end);
	int count(const T &item);
	void remove(const T &item);
	MyList &operator=(const MyList &l);
	MyList &operator+=(const T &item);
	MyList &operator+=(const MyList &l);
	T &operator[](int index);
	void sort(bool less=true);
	void reverse();
	~MyList(){delete [] a;}
};

template<class T>
MyList<T> operator+(const MyList<T> &l1, const MyList<T> &l2){
	MyList<T> tmp=l1;
	tmp.len += l2.len;
	while (tmp.len>tmp.size) tmp.double_space();
	for (int i=0;i<l2.len;++i) tmp.a[l1.len+i] = l2.a[i];
	return tmp;
}

template<class T>
MyList<T> operator+(const MyList<T> &l1, const T &item){
	MyList<T> tmp=l1;
	tmp.len += 1;
	if (tmp.len>tmp.size) tmp.double_space();
	tmp.a[tmp.len-1] = item;
	return tmp;
}

template<class T>
ostream &operator<<(ostream &os, const MyList<T> &obj){
	if (obj.len==0) os << "[]";
	else{os << '[' ; for (int i=0;i<obj.len-1;++i) os << obj.a[i] << ',' << ' '; os << obj.a[obj.len-1] << ']';}
	return os; 
}

template<class T>
void MyList<T>::double_space(){
	size = 2*size;
	T *tmp = new T [size];
	for (int i=0;i<len;++i) tmp[i]=a[i];
	delete [] a;
	a = new T [size];
	for (int i=0;i<len;++i) a[i]=tmp[i];
	delete [] tmp;
}

template<class T>
MyList<T>::MyList(const MyList<T> &l){
	size = l.size;
	len = l.len;
	a = new T [size];
	for (int i=0;i<len;++i) a[i] = l.a[i];
}

template<class T>
MyList<T>::MyList(int num, const T &item){
	size = 100;
	len = num;
	a = new T [size];
	while (len>size) double_space();
	for (int i=0;i<num;++i) a[i] = item;
}

template<class T>
MyList<T>::MyList(const MyList<T> &l, int n){
	try{
		if (l.len<n) throw 1;
		size = 100;
		len = n;
		a = new T [size];
		while (len>size) double_space();
		for (int i=0;i<n;++i) a[i] = l.a[i];
	}
	catch (int) {
		cout << "Out of range! Creation is invalid!" << endl;
	}
}

template<class T>
void MyList<T>::push(const T &item){
	len += 1;
	if (len>size) double_space();
	a[len-1] = item;
}

template<class T>
T MyList<T>::pop(){
	try{
		if (len==0) throw 1;
		T tmp=a[len-1];
		--len;
		return tmp;
	}
	catch (int){
		cout << "List is empty! Pop is invalid!" << endl;
	}
}

template<class T>
void MyList<T>::insert(int index, const T &item){
	try{
		if (index<0 || index>len-1) throw 1;
		len += 1;
		if (len>size) double_space();
		for (int i=len-1;i>index-1;--i) a[i+1] = a[i];
		a[index] = item; 
	}
	catch (int){
		cout << "Index is out of range! Insert is invalid!" << endl;
	}
}

template<class T>
void MyList<T>::clean(){
	len = 0;
}

template<class T>
int MyList<T>::get_size(){
	return len;
}

template<class T>
void MyList<T>::erase(int start, int end){
	try{
		if (start<0 || start>end || end>len-1) throw 1;
		len -= (end-start+1);
		for (int i=end+1;i<end+1+len-start;++i) a[i-end-1+start] = a[i];
	}
	catch (int){
		cout << "Out of range! Delete is invalid!" << endl;
	}
}

template<class T>
T MyList<T>::get_item(int index){
	try{
		if (index<0 || index>len-1) throw 1;
		return a[index];
	}
	catch (int){
		cout << "Index is uut of range! Get is invalid!" << endl;
	}
}

template<class T>
MyList<T> MyList<T>::get_item(int start, int end){
	try{
		int min=0-len, max=len-1;
		if (start<min || start>max || end<min || end>max) throw 1;
		if (start<0) start += len;
		if (end<0) end += len;
		MyList tmp;
		if (start>end){
			tmp.len = 0;
		}else{
			tmp.len = end-start+1;
			while (tmp.len>tmp.size) tmp.double_space();
			for (int i=start;i<=end;++i){
				tmp.a[i-start] = a[i];
			}
		}
		return tmp;
	}
	catch (int){
		cout << "Out of range! Get is invalid!" << endl;
	}
}

template<class T>
int MyList<T>::count(const T &item){
	int cnt=0;
	for (int i=0;i<len;++i){
		if (a[i]==item) ++cnt;
	}
	return cnt;
}

template<class T>
void MyList<T>::remove(const T &item){
	int index=-1;
	for (int i=0;i<len;++i){
		if (a[i]==item){
			index = i; break;
		}
	}
	if (index!=-1){
		--len;
		for (int i=index+1;i<len+1;++i) a[i-1] = a[i];
	}
}

template<class T>
MyList<T> &MyList<T>::operator=(const MyList &l){
	if (this == &l) return *this;
	delete [] a;
	size = l.size;
	len = l.len;
	a = new T [size];
	for (int i=0;i<len;++i) a[i] = l.a[i];
	return *this;
}

template<class T>
MyList<T> &MyList<T>::operator+=(const T &item){
	++len;
	if (len>size) double_space();
	a[len-1] = item;
	return *this;
}

template<class T>
MyList<T> &MyList<T>::operator+=(const MyList &l){
	len += l.len;
	while (len>size) double_space();
	for (int i=0;i<l.len;++i) a[len-l.len+i] = l.a[i];
	return *this;
}

template<class T>
T &MyList<T>::operator[](int index){
	try{
		if (index<0 || index>len-1) throw 1;
		return a[index];
	}
	catch (int){
		cout << "The index is out of range!" << endl;
	}
}

template<class T>
void MyList<T>::sort(bool less/*=true*/){
	quicksort(a,0,len-1);
	if (less!=true) inverse(a,len);
}

template<class T>
void MyList<T>::reverse(){
	inverse(a,len);
}

template<class T>
void quicksort(T a[], int low, int high){
	int mid;
	if (low>=high) return;
	mid = divide(a,low,high);
	quicksort(a,low,mid-1);
	quicksort(a,mid+1,high);
}

template<class T>
int divide(T a[], int low, int high){
	T k=a[low];
	do {
		while (low<high&&a[high]>=k) --high;
		if (low<high){a[low] = a[high]; ++low;}
		while (low<high&&a[low]<=k) ++low;
		if (low<high){a[high]=a[low]; --high;}
	}while (low!=high);
	a[low]=k;
	return low;
}

template<class T>
void inverse(T a[], int n){
	T tmp;
	for (int i=0;i<n/2;++i){
		tmp = a[i];
		a[i] = a[n-1-i];
		a[n-1-i] = tmp;
	}
}

int main(){
	MyList<int> a, b;
	int i;
	for (i=0; i<5; ++i)
		a.push(i);
    // a = [0, 1, 2, 3, 4]
	a[3] = 15; // a = [0, 1, 2, 15, 4]
	a.sort(); // a = [0, 1, 2, 4, 15]
	a.reverse(); // a = [15, 4, 2, 1, 0]
	a += 12; // a = [15, 4, 2, 1, 0, 12]
	for (i=0; i<a.get_size(); ++i)
		cout<<a[i]<<endl;
    b = a.get_item(4, -3); // b = [] 
	b = a.get_item(3, -1); // b = [1, 0, 12] 
	a += b; // a = [15, 4, 2, 1, 0, 12, 1, 0, 12]
	for (i=0; i<a.get_size(); ++i)
		cout<<a.get_item(i)<<endl;
	cout<<a.count(5)<<endl;
	b.clean(); // b = []
	cout<<b.get_size()<<endl;
	a.erase(2, 5); // a = [15, 4, sth is wrong here:1, 0, 12]
	b = a + a; // b = [15, 4, 0, 12, 15, 4, 0, 12]
	b.insert(3, 116); // b = [15, 4, 0, 116, 12, 15, 4, 0, 12]
	b.remove(4); // b = [15, 0, 116, ...]
	cout<<b<<endl;
	
	MyList<double> c(10, 3.14);
	for (i=0; i<100; ++i)
		c.push(1.1*i);
	cout<<c.get_item(100, 105)<<endl;
	return 0;
}
