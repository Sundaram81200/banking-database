#include<fstream.h>
#include<ctype.h>
#include<process.h>
#include<conio.h>
#include<stdio.h>
#include<string.h>
struct date
	{ int dd;
	  int mm;
	  int yy;
	};

class bank
{
 long acno;		//Account Number
  char name[20];	//Name of Account Holder
  float opbal;		//Opening Balance for Account
  char type;        	//Type of Account C-Current, S-Saving
  float amt;		//Amount of deposit/withdraw
  float balance; 	//Balance amount in account
  char mo[11];	//Mobile number
  date doa;    	//date of opening account
  date dot;		//date of transaction
  char ttype;		//Transaction type - D-deposit, W-Withdraw

  public:
  bank()
  {
   acno=0;
   strcpy(name,NULL);
   opbal=0;
   type='S';
   amt=0;
   balance=0;
   strcpy(mo,NULL);
   ttype=' ';
  }
  void createac(int m)
  { acno=m;
    cout<<"Account No. "<<acno;
    cout<<"\nEnter Name: ";
    gets(name);
    cout<<"\nEnter type of Account (C-Current/ S-Saving)";
    cin>>type;
    cout<<"\nEnter Date of Opening Account (dd/mm/yy)";
    cin>>doa.dd>>doa.mm>>doa.yy;
    cout<<"\nEnter Mobile No: ";
    cin>>mo;
    cout<<"\nEnter Opening Balance:";
    cin>>opbal;
    balance=opbal;
  }

 //Display only basic account details
 void disp()
 {  cout<<"\n================================\n";
    cout<<"\n\nAccount Number: "<<acno;
    cout<<"\nName: "<<name;
    cout<<"\nType of Account: "<<type;
    cout<<"\nDate of Opening Account: "<<doa.dd<<"/"<<doa.mm<<"/"<<doa.yy;
    cout<<"\nMobile Number: "<<mo;
    cout<<"\nBalance Amount: "<<balance;
   }

 //Display the transaction details
 void display()
 {  cout<<"\n================================";
    cout<<"\n\nAccount Number: "<<acno;
    cout<<"\tName: "<<name;
    cout<<"\tType of Account: "<<type;
    cout<<"\nDate of Opening Account: "<<doa.dd<<"/"<<doa.mm<<"/"<<doa.yy;
    cout<<"\tMobile Number: "<<mo;
    cout<<"\nMode of transaction: "<<ttype;
    cout<<"\tAmount: "<<amt;
    cout<<"\tDate of Transaction: "<<dot.dd<<"/"<<dot.mm<<"/"<<dot.yy;
    cout<<"\nBalance Amount: "<<balance;
   }
char* retname()
  {
    return name;
  }

long retacno()
 {
   return acno;
 }

 char rettype()
 {
   return ttype;
 }

   void transac();
};

 void bank::transac()
   {cout<<"\nEnter D-Deposit, W-Withdraw: ";
    cin>>ttype;
    ttype=toupper(ttype);
    cout<<"\n Enter amount"<<endl;
    cin>>amt;
    cout<<"\nEnter date of transaction (dd/mm/yyyy)";
    cin>>dot.dd>>dot.mm>>dot.yy;

    if(ttype=='D')
     { balance+=amt; cout<<"\Balance: "<<balance; }
    else if(ttype=='W')
     { if(balance>amt+2000)
       	balance-=amt;
      else
       	cout<<"No sufficient balance";
     }
     else
     { cout<<"Entered wrong choice";
     }

   }
bank b;

 ofstream f;
 ifstream f1;
 fstream f2;

 void writeinto()	//open binary file and create new account no.
 {
     int n;
     f1.open("bank.dat",ios::binary);
     f1.seekg(0,ios::end);
     n=f1.tellg()/sizeof(b);
     f1.close();
     b.createac(n+1);
     f.open("bank.dat",ios::binary|ios::app);
     f.write((char*)&b,sizeof(b));
     f.close();
 }

 void searchbyacno()
 {  long x;
    int flag=0;
    cout<<"\nEnter Account number to be located: ";
    cin>>x;
    f1.open("bank.dat");
    while(f1.read((char*)&b,sizeof(b)))
	{
     if(b.retacno()==x)
	{
	 b.disp();
	 flag=1;
	 }
    }
    if(flag==0)
	   cout<<"\nNo such record exists";

    f1.close();
 }


 void searchbyName()
 {  char x[20]; int flag=0;
    cout<<"\nEnter name to be located: ";
    gets(x);
    f1.open("bank.dat");

    while(f1.read((char*)&b,sizeof(b)))
    { if(strcmpi(b.retname(),x)==0)
	{
	 flag=1;
	 b.disp();
	 }
    }
    if(flag==0)
	   cout<<"\nNo such record";
    f1.close();
 }

 void displayall()
 { f1.open("bank.dat");
   while(f1.read((char*)&b,sizeof(b)))
   {
    b.disp();
    }
   f1.close();
 }

 //All Transactions to be displayed as per account no and transaction type
 void displayall1()
 { f1.open("trans.dat");
   long a; char tt;
   cout<<"\nEnter account no: "; cin>>a;
   cout<<"\nEnter transaction type (D/W): "; cin>>tt;
   tt=toupper(tt);
   while(f1.read((char*)&b,sizeof(b)))
   {  if(b.retacno()==a && b.rettype()==tt)
		b.display();
    }
   f1.close();
 }
 //Deposit or withdrawal
void transaction()
 {
  ofstream f3("trans.dat",ios::binary|ios::app);
  long x;
  int flag=0;
  cout<<"\nEnter account number: ";
  cin>>x;
  f2.open("bank.dat",ios::binary|ios::in|ios::out);
  while(f2.read((char*)&b, sizeof(b)))
  {
   if(b.retacno()==x)
   {
    flag=1;
    clrscr();
    b.disp();
    b.transac();
     int pos=(-1)*sizeof(b);
    f2.seekp(pos,ios::cur);
    f2.write((char*)&b,sizeof(b));
    f3.write((char*)&b,sizeof(b));
   }
  }
  f2.close();
  f3.close();
  if(flag==0)
   cout<<"\nNo such record exists";
 }

 void menu()
 {
  clrscr();
  gotoxy(5,5);
  cout<<"ษออออออออออออออออออออออออออออออออออออออออออออออออออป\n";
  gotoxy(5,8);
  cout<<"บ                                                  บ\n";
  gotoxy(5,9);
  cout<<"บ                 BANKING (C++)                    บ\n";
  gotoxy(5,10);
  cout<<"บ                                                  บ\n";
  gotoxy(5,11);
  cout<<"บ                 DONE BY:                         บ\n";
  gotoxy(5,12);
  cout<<"บ                      Sundaram                    บ\n";
  gotoxy(5,13);
  cout<<"บ                                                  บ\n";
  gotoxy(5,17);
  cout<<"ศออออออออออออออออออออออออออออออออออออออออออออออออออผ\n";
  getch();
 }

 void main()
 {
  menu();
  clrscr();
  char ch;
  do
   {
     clrscr();
     cout<<"MAIN MENU"<<endl
	 <<"ออออออออออออออออออออออออออออออออออออออออออออออออ"<<endl;
     cout<<"1. Create New Account "<<endl
	 <<"2. Display All Account Details "<<endl
	 <<"3. Search by Account Number "<<endl
	 <<"4. Search by Name "<<endl
	 <<"5. Transaction (Deposit/Withdraw) "<<endl
	 <<"6. Detailed statement "<<endl
	 <<"7. Exit "<<endl;
       int n;
       cout<<"Enter your choice (1-7): ";
       cin>>n;
       switch(n)
       { case 1:clrscr();
		writeinto();
		b.disp();
		break;
	 case 2:clrscr();
		displayall();
		break;
	 case 3:clrscr();
		searchbyacno();
		break;
	 case 4:clrscr();
		searchbyName();
		break;
	 case 5:clrscr();
		transaction();
		break;
	 case 6:clrscr();
		displayall1();
		break;
	 case 7:exit(0);
	 default: cout<<"wrong";
	 }
	 cout<<"\n\nDo you wish to continue(y/n): ";
	 cin>>ch;
  } while(ch=='y'||ch=='Y');

  getch();
  }

