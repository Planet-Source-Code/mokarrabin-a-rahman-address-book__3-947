<div align="center">

## Address book


</div>

### Description

Simple address book Class in C++, has methods for adding new record, sorting, deleting and storing data in a file. Has it own menu aswell.
 
### More Info
 


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Mokarrabin A Rahman](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/mokarrabin-a-rahman.md)
**Level**          |Beginner
**User Rating**    |3.4 (17 globes from 5 users)
**Compatibility**  |C, C\+\+ \(general\), Microsoft Visual C\+\+, Borland C\+\+, UNIX C\+\+
**Category**       |[Databases](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/databases__3-5.md)
**World**          |[C / C\+\+](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/c-c.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/mokarrabin-a-rahman-address-book__3-947/archive/master.zip)





### Source Code

```
//**********************************************
//	The address book
//	mokarrabin@mail.com
//	http://www.geocities.com/mokarrabin
//**********************************************
# define maxAdd  100
# include<iostream.h>
# include  <conio.h>
# include <fstream.h>
# include <string.h>
# include   <dos.h>
class adbk{
 struct data{
  char name  [20];
  char address[30];
  char tel  [12];
  char fax  [12];
  char email [26];
 }info[maxAdd],temp;
 int count,n,PTR;char ch;
public:
  //Constructor that reads all the previous data stored in File.
  adbk(){
	 clrscr();cout<<"Reading data..";delay(1000);
	 count=0;n=0;
	//read all the data from HDD.
	ifstream in("adbk.dat");
	while(in.read((char *)&temp,sizeof(temp))!=0){
	 strcpy(info[count].name,temp.name);strcpy(info[count].address,temp.address);
	 strcpy(info[count].tel,temp.tel);strcpy(info[count].fax,temp.fax);
	 strcpy(info[count].email,temp.email);
	 if(temp.name[0]!=' ')count++;
	}
	in.close();cout<<"done.\n\n";delay(100);
  };
  //Destructor that truncates the older data file and writes the new data
  ~adbk(){		cout<<"Writing data to file..";
	//Write all data to HDD.
	ofstream out("adbk.dat",ios::trunc|ios::binary);
	for(n=0;n<count;n++){
	 out.write((char *)&info[n],sizeof(info[n]));
	}
	out.close();cout<<"Finished\n\n";delay(1000);
  };
  //Method to get new data from the user & keep it in memory.
  getNew(){
	cout<<"Name:";cin>>temp.name;cout<<endl;
	cout<<"Address:";cin>>temp.address;cout<<endl;
	cout<<"Tel:";cin>>temp.tel;cout<<endl;
	cout<<"Fax:";cin>>temp.fax;cout<<endl;
	cout<<"Email:";cin>>temp.email;cout<<endl;
	 strcpy(info[count].name,temp.name);strcpy(info[count].address,temp.address);
	 strcpy(info[count].tel,temp.tel);strcpy(info[count].fax,temp.fax);
	 strcpy(info[count].email,temp.email);
	 count++;
  };
  //Method to show & edit all the data from the memory
  // this function returns an integer value that is used as command in the
  // main boy of the program.
int showNedit(){     n=0;
	//Show the records
	while(ch!=27){					clrscr();
	 cout<<"<ESC>Escape.\n<D>Delete Record.\n<U arrow>Up <D arrow>Down\n";
	 cout<<"<A>Add New Record\n<S>Sort Database\n";
	 cout<<"\nRecord Num:"<<n+1<<"\n\n";
	 cout<<info[n].name<<endl<<info[n].address<<endl<<info[n].tel<<endl;
	 cout<<info[n].fax<<endl<<info[n].email<<endl;
	 ch=getch();clrscr();//if(ch==0)ch=getch();
	 if (ch==72 && n>0)n--;
	 if (ch==80 && n<count-1)n++;
	 if (ch=='d'||ch=='D'){//delete a record.
	   temp=info[n];
	   info[n]=info[count-1];
	   count--; return 1;
	 }
	 if(ch=='a'||ch=='A')return 2;
	 if(ch=='s'||ch=='S')return 1;
	}
	return 0;//Return the total num of records.
  };//end of retreive
  //Method to sort the records list in memory.
  sort(){
    //Bubble Sort from 'DATA STRUCURES' by SEYMOUR & LIPSCHUTZ.
	for(n=1;n<count-1;n++){
	 PTR=1;
	 while(PTR<=count-n){
	 if(strcmp(info[PTR-1].name,info[PTR].name)>0){
	  temp=info[PTR-1];
	  info[PTR-1]=info[PTR];
	  info[PTR]=temp;}
	 PTR++;
	 }
	}
//------
  }
}ob;
main() {
  int command=205;
  while(command!=0){
   command= ob.showNedit();//returns a value.
   if(command==1)ob.sort();
   if(command==2){
	ob.getNew();
	ob.sort();
   }
  }
}
```

