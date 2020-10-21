# LIBRARY-MANAGEMNET-CPP
##**This is used to various colleges or scholls for their library management as well as many student can use this as project**
#include<fstream>
#include<conio.h>
#include<iostream>
#include<iomanip>
#include<string.h>
#include<windows.h>
using namespace std;

class Library
{
 int BookId;
  char Title[20];
  char Author[20];
  char Category[20];
  int Pages;
  float Price;
 public:
 int getID(){return BookId;}
  char* getTitle(){return Title;}
  char* getAuthor(){return Author;}
  char* getCategory(){return Category;}
  float getPrice(){return Price;}
 Library()
  {
   BookId=0;
   strcpy(Title,"");
   strcpy(Author,"");
   strcpy(Category,"");
  Pages=0;
   Price=0;
 }
 
 void getBook();
 void listView();
 void showBook();
 void header();
}l;

void Library::getBook()
{
 cout<<"\tEnter Book Id : ";
 cin>>BookId;
 cout<<"\tEnter Book Title : ";
 cin.get();
 cin.getline(Title,20);
 cout<<"\tEnter Book Author: ";
 cin.getline(Author,20);
 cout<<"\tEnter Book Category: ";
 cin.getline(Category,20);
 cout<<"\tEnter No. of Pages : ";
 cin>>Pages;
 cout<<"\tEnter Price of Book: ";
 cin>>Price;
 cout<<endl;
}
void Library::showBook()
{
 cout<<endl;
 cout<<"Book ID      : "<<BookId<<endl;
 cout<<"Book Title   : "<<Title<<endl;
 cout<<"Author Name  : "<<Author<<endl;
 cout<<"Category     : "<<Category<<endl;
 cout<<"No. of Pages : "<<Pages<<endl;
 cout<<"Price of Book: "<<Price<<endl;
}
void Library::header()
{
 cout.setf(ios::left);
 cout<<setw(5)<<"I.D."
  <<setw(20)<<"Book Title"
  <<setw(20)<<"Book Author"
  <<setw(15)<<"Category"
  <<setw(6)<<"Pages"
  <<setw(6)<<"Price"<<endl;
 for(int i=1;i<=72;i++)
  cout<<"=";
 cout<<endl;
}
void Library::listView()
{
 cout.setf(ios::left);
 cout<<setw(5)<<BookId
  <<setw(20)<<Title
  <<setw(20)<<Author
  <<setw(15)<<Category
  <<setw(6)<<Pages
  <<setw(6)<<Price<<endl;
}
void heading();  
void menu();  
void searchMenu(); 
void addBook();  
void displayBooks();
void searchByID(); 
void searchByTitle();
void searchByCategory();
void searchByPrice();
void searchByAuthor(); 
void modify();  
void displayDisposed();
void heading()
{
 cout<<"\t\tL I B R A R Y   M A N A G E M E N T   S Y S T E M\n";
}
void addBook()
{
 ofstream fout;
 fout.open("books.dat",ios::app);
 l.getBook();
 fout.write((char*)&l,sizeof(l));
 cout<<"Book data saved in file...\n";
 cout<<"\t\t\t\t\t**PROJECT IS MADE BY SOURAV CHOUDHARY**";
 fout.close();
} 
void displayBooks()
{
 ifstream fin("books.dat");
 int rec=0;
 while(fin.read((char*)&l,sizeof(l)))
 {
  if(rec<1)
   l.header();
  l.listView();
  rec++;
 }
 fin.close();
 cout<<"\nTotal "<<rec<<" Records in file...\n";
 cout<<"\t\t\t\t\t**PROJECT IS MADE BY SOURAV CHOUDHARY** ";
}
void searchByID()
{
 int n,flag=0;
 ifstream fin("books.dat");
 cout<<"Enter Book ID : ";
 cin>>n;
 while(fin.read((char*)&l,sizeof(l)))
 {
  if(n==l.getID())
  {
   l.showBook();
   flag++;
  }
 }
 fin.close();
 if(flag==0)
  cout<<"Book Number with ID:"<<n<<" not available...\n";
  cout<<"\t\t\t\t\t**PROJECT IS MADE BY SOURAV CHOUDHARY** ";
}
void searchByTitle()
{
 int flag=0;
 char title[20];
 ifstream fin("books.dat");
 cout<<"Enter Book Title : ";
 cin.ignore();
 cin.getline(title,20);
 while(fin.read((char*)&l,sizeof(l)))
 {
  if(strcmpi(title,l.getTitle())==0)
  {
   l.showBook();
   flag++;
  }
 }
 fin.close();
 if(flag==0)
  cout<<"Book with Title: "<<title<<" not available...\n";
  cout<<"\t\t\t\t\t**PROJECT IS MADE BY SOURAV CHOUDHARY**";
}
void searchByCategory()
{
 int flag=0,rec=0;
 char cat[20];
 ifstream fin("books.dat");
 cout<<"Enter Book Category : ";
 cin.ignore();
 cin.getline(cat,20);
 while(fin.read((char*)&l,sizeof(l)))
 {
  if(strcmpi(cat,l.getCategory())==0)
  {
   if(rec<1)
    l.header();
   l.listView();
   flag++;
   rec++;
  }
 }
 fin.close();
 if(flag==0)
  cout<<"Book with Category: "<<cat<<" not available...\n";
  cout<<"\t\t\t\t\t**PROJECT IS MADE BY SOURAV CHOUDHARY** ";
}
void searchByAuthor()
{
 int flag=0,rec=0;
 char aut[20];
 ifstream fin("books.dat");
 cout<<"Enter Book Author : ";
 cin.ignore();
 cin.getline(aut,20);
 while(fin.read((char*)&l,sizeof(l)))
 {
  if(strcmpi(aut,l.getAuthor())==0)
  {
   if(rec<1)
    l.header();
   l.listView();
   flag++;
   rec++;   
  }
 }
 fin.close();
 if(flag==0)
  cout<<"Book with Author name: "<<aut<<" not available...\n";
  cout<<"\t\t\t\t\t**PROJECT IS MADE BY SOURAV CHOUDHARY** ";
}
void searchByPrice()
{
 int flag=0,rec=0;
 float minrate, maxrate;
 ifstream fin("books.dat");
 cout<<"Enter Minimum Price of Book : ";
 cin>>minrate;
 cout<<"Enter Maximum Price of Book : ";
 cin>>maxrate;
 
 while(fin.read((char*)&l,sizeof(l)))
 {
  if(l.getPrice()>=minrate && l.getPrice()<=maxrate)
  {
   if(rec<1)
    l.header();
   l.listView();
   flag++;
   rec++;
  }
 }
 fin.close();
 if(flag==0)
  cout<<"Books between Price Range: "<<minrate
      <<" and "<<maxrate<<" not available...\n";
  cout<<"\t\t\t\t\t**PROJECT IS MADE BY SOURAV CHOUDHARY** ";
}
void dispose()
{
 int n,flag=0;
 ifstream fin("books.dat");
 ofstream fout("dispose.dat",ios::out);
 cout<<"Enter Book ID : ";
 cin>>n;
 while(fin.read((char*)&l,sizeof(l)))
 {
  if(n==l.getID())
  {
   l.showBook();
   flag++;
  }
  else
  {
   fout.write((char*)&l,sizeof(l));
  }
 }
 fin.close();
 fout.close();
 if(flag==0)
  cout<<"Book Number with ID:"<<n<<" not available...\n"; 
  cout<<"\t\t\t\t\t\t\t\n**PROJECT IS MADE BY SOURAV CHOUDHARY** ";
}
void modify()
{
 int n,flag=0,pos;
 fstream fin("books.dat",ios::in|ios::out);
 cout<<"Enter Book ID : ";
 cin>>n;
 while(fin.read((char*)&l,sizeof(l)))
 {
  if(n==l.getID())
  {
   pos=fin.tellg();
   cout<<"Following data will be edited...\n";
   l.showBook();
   flag++;
   fin.seekg(pos-sizeof(l));
   l.getBook();
   fin.write((char*)&l,sizeof(l));
   cout<<"\nData Modified successfully...\n";
   cout<<"\t\t\t\t\t\t\t\n**PROJECT IS MADE BY SOURAV CHOUDHARY** ";
  }
 }
 fin.close();
 if(flag==0)
  cout<<"Book Number with ID:"<<n<<" not available...\n";
  cout<<"\t\t\t\t\t\t\t\n**PROJECT IS MADE BY SOURAV CHOUDHARY** ";
}
void displayDisposed()
{
 ifstream fin("dispose.dat");
 int rec=0;
 while(fin.read((char*)&l,sizeof(l)))
 {
  if(rec<1)
   l.header();
  l.listView();
  rec++;
 }
 fin.close();
 cout<<"\nTotal "<<rec<<" Records in disposed off file...\n";
 cout<<"\t\t\t\t\t\t\t\n**PROJECT IS MADE BY SOURAV CHOUDHARY** ";
}
void menu()
{
 int ch;
 do
 {
  system("cls");
  heading();
  cout<<"0. EXIT.\n";
  cout<<"1. Add New Book\n";
  cout<<"2. Display All Books\n";
  cout<<"3. Search Books\n";
  cout<<"4. Disposed Off Books\n";
  cout<<"5. Modify Details\n";
  cout<<"6. List of Disposed Books\n";
  cout<<"Enter Your Choice : ";
  cin>>ch;
  system("cls");
  heading();
  switch(ch)
  {
   case 1: addBook(); break;
   case 2:  displayBooks(); break;
   case 3:  searchMenu(); break;
   case 4:  dispose(); break;
   case 5:  modify(); break;
   case 6:  displayDisposed(); break;
  }
  system("pause");
 }while(ch!=0);
}

void searchMenu()
{
 int ch;
 do
 {
  system("cls");
  heading();
  cout<<"BOOK SEARCH OPTIONS\n";
  cout<<"0. Back\n";
  cout<<"1. By ID\n";
  cout<<"2. By Title\n";
  cout<<"3. By Category\n";
  cout<<"4. By Author\n";
  cout<<"5. By Price Range\n";
  cout<<"Enter Your Choice : ";
  cin>>ch;
  system("cls");
  heading();
  switch(ch)
  {
   case 1: searchByID(); break;
   case 2:  searchByTitle(); break;
   case 3:  searchByCategory(); break;
   case 4:  searchByAuthor(); break;
   case 5:  searchByPrice();break;
   default: cout<<"\a";
  }
  system("pause");
 }while(ch!=0);
}
int main()
{
	int i,j,k;
	cout<<"\n";
	system("color 7A");
	cout<<"\t#########################################################\n";
	cout<<"\t |                                                      |\n";
	cout<<"\t |**WELCOME TO C++ PROGRAM OF LIBRARY MANAGEMENT SYSTEM |**\n";
	cout<<"\t |             DEVELOPED BY SOURAV CHOUDHARY            |\n";
	cout<<"\t#########################################################\n";
	for(i=0;i<5;i++)
	{
		cout<<".";
		Sleep(1000);
	}
	system("cls");
	cout<<"\n";
	system("color 6b");
	cout<<"\n\n\t## WELCOME TO CPP PROGRAM LIBRARY MANAGEMNET SYSTEM ##\n\n\n";
	cout<<"\nPRESS ANY KEY TO START\n";
	for(i=0;i<5;i++)
	{
		cout<<".";
		Sleep(1000);
	}
	fflush(stdin);
	system("cls");
	system("color 3E");
    menu();
    return 0;
}

