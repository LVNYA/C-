SOURCE CODE
#include<iostream.h>
#include<conio.h>
#include<stdio.h>
#include<fstream.h>
#include<string.h>

class PATIENT
{
char ptname[30];

public:
char dept[30],doct[30],status[30],disease[30],sex,gnm[30],add[50],doa[10];
int age,
int roomno;
int ptuid;

void input()                               //To input patient's details
{
clrscr();
cout<<endl<<"/\\/\\/\\/\\/\\/\\/\\/\\/\\/\\/\\/\\/"<<endl;
cout<<"<  Enter Patient Details  >"<<endl;
cout<<"\\/\\/\\/\\/\\/\\/\\/\\/\\/\\/\\/\\/\\"<<endl<<endl;
cout<<"#UID                  :";
cin>>ptuid;
cout<<"Name                  :";
gets(ptname);
cout<<"Age                   :";
cin>>age;
cout<<"Sex (M/F)             :";
cin>>sex;
cout<<"Guardian name         :";
gets(gnm);
cout<<"Residence             :";
gets(add);
cout<<"DateOfAdmn(dd-mm-yyyy):";
gets(doa);
cout<<"Doctor's name         :";
gets(doct);
cout<<"Department            :";
gets(dept);
cout<<"Disease               :";
gets(disease);
cout<<"Status                :";
gets(status);
cout<<"Room No.              :";
cin>>roomno;
}

void output()                              //To display patient's details
{
clrscr();
cout<<"/\\/\\/\\/\\/\\/\\/\\/\\/\\/\\/\\/"<<endl;
cout<<"<   Patient Details   >"<<endl;
cout<<"\\/\\/\\/\\/\\/\\/\\/\\/\\/\\/\\/"<<endl<<endl;
cout<<"#UID                  :"<<ptuid<<endl;
cout<<"Name                  :"<<ptname<<endl;
cout<<"Age                   :"<<age<<endl;
cout<<"Sex (M/F)             :"<<sex<<endl;
cout<<"Guardian name         :"<<gnm<<endl;
cout<<"Residence             :"<<add<<endl;
cout<<"DateOfAdmn(dd-mm-yyyy):"<<doa<<endl;
cout<<"Doctor's name         :"<<doct<<endl;
cout<<"Department            :"<<dept<<endl;
cout<<"Disease               :"<<disease<<endl;
cout<<"Status                :"<<status<<endl;
cout<<"Room No.              :"<<roomno<<endl;
}

void change_status(char stat[])            //To change status
{
strcpy(status,stat);

}

void change_disease(char d[])              //To change disease
{
strcpy(disease,d);
}

char* retname()                            //To retun private member patient name
{
return (ptname);
}

void disp()	                           // for uid ptname
{ //clrscr();
cout<<"\n Patient's #UID: "<<ptuid;
cout<<"\nPatient's name: "<<ptname;
}

};


void create_ptf()                          //To create file and enter data
{
clrscr();
fstream f;
f.open("PATIENT.dat",ios::binary|ios::app);
PATIENT p;
char ch;
do
{
cout<<"Enter the pateint's details:\n";
p.input();
f.write((char*)&p,sizeof(p));
cout<<"Do you want to enter more data(y/n):";
cin>>ch;
}while(ch!='n');
f.close();
cout<<"\nPress any key to return to main menu";
getch();
}

void disp_ptf()                         //To display patient name and #UID
{
clrscr();
fstream f;
f.open("PATIENT.dat",ios::binary|ios::in);
PATIENT p;
while(f.read((char*)&p,sizeof(p)))
{
p.disp();
}
f.close();
cout<<"\nPress any key to return to main menu";
getch();
}

void disp_dept()                            //To display departments in the hospital
{
clrscr();
cout<<"The DEPARTMENTS in our Hospital are:\n";
cout<<"1.  General Medicine\n";
cout<<"2.  Pediatrics\n";
cout<<"3.  Dermatology\n";
cout<<"4.  Psychiatry\n";
cout<<"5.  Chest & TB\n";
cout<<"6.  General Surgery\n";
cout<<"7.  Orthopedics\n";
cout<<"8.  Ophthalmology\n";
cout<<"9.  ENT\n";
cout<<"10. Obst. & Gynaecology\n";
cout<<"\nPress any key to return to main menu";
getch();
}

void search_ptnm()                         //search by patient's name
{
clrscr();
fstream f;
f.open("PATIENT.dat",ios::binary|ios::in);
char nm[30];
cout<<"Enter name of Patient to search:\n";
gets(nm);
PATIENT p;
int flag=0;
while(f.read((char*)&p,sizeof(p)))
 {  if(strcmpi(nm,p.retname())==0)
     {
     p.output();
     flag++;
     }
  }
if (!flag)
   cout<<"Patient not found\n";
f.close();
cout<<"\nPress any key to return to search menu";
getch();
}

void search_ptuid()                        //search by #uid
{
clrscr();
fstream f;
f.open("PATIENT.dat",ios::binary|ios::in);
int no;
cout<<"Enter #UID of Patient to search:";
cin>>no;
PATIENT p;
int flag =0;
cout<<"Patient with #UID "<<no<<" is ";
while(f.read((char*)&p,sizeof(p)))
  {
    if(p.ptuid==no)
    {
	 p.output();
	 flag++;
     }
   }
if(!flag)
  cout<<"Patient not found\n";
f.close();
cout<<"\nPress any key to return to search menu";
getch();
}

void search_ptdoc()                        //search by doctor name
{
clrscr();
fstream f;
f.open("PATIENT.dat",ios::binary|ios::in);
char docnm[30];
cout<<"Enter the Doctor's name: ";
gets(docnm);
PATIENT p;
int flag=0;
cout<<"Patients under "<<docnm<<" are:\n";
while(f.read((char*)&p,sizeof(p)))
{
   if(strcmpi(p.doct,docnm)==0)
   {
      p.disp();
      flag++;
    }
}
if(!flag)
  cout<<"There is no patient under "<<docnm<<"\n";
f.close();
cout<<"\nPress any key to return to search menu";
getch();
}

void search_ptdis()                        //search by disease
{
clrscr();
fstream f;
f.open("PATIENT.dat",ios::binary|ios::in);
char dis[30];
cout<<"Enter the disease :";
gets(dis);
PATIENT p;
int flag=0;
while(f.read((char*)&p,sizeof(p)))
{
  if(strcmpi(p.disease,dis)==0)
  {
     p.disp();
     flag++;
  }
}
if(!flag)
  cout<<"There is no patient having "<<dis<<" disease\n";
f.close();
cout<<"\nPress any key to return to search menu";
getch();
}

void search_ptdept()                        //search by disease
{
clrscr();
fstream f;
f.open("PATIENT.dat",ios::binary|ios::in);
char dep[30];
cout<<"Enter the disease :";
gets(dep);
PATIENT p;
int flag=0;
while(f.read((char*)&p,sizeof(p)))
{
  if(strcmpi(p.dept,dep)==0)
  {
     p.disp();
     flag++;
  }
}
if(!flag)
  cout<<"There is no patient in "<<dep<<" department\n";
f.close();
cout<<"\nPress any key to return to search menu";
getch();
}
void search_menu()                         //Search menu
{
int c;
do
{
clrscr();
cout<<"SEARCH PATIENT BY: \n";
cout<<"1.  Name\n";
cout<<"2.  #UID\n";
cout<<"3.  Doctor\n";
cout<<"4.  Disease\n";
cout<<"5.  Department\n";
cout<<"6.  Quit\n\n";
cout<<"Enter your choice: \n";
cin>>c;
switch (c)
   {
     case 1: search_ptnm(); break;
     case 2: search_ptuid(); break;
     case 3: search_ptdoc(); break;
     case 4: search_ptdis(); break;
     case 5: search_ptdept(); break;
     case 6: break;
   }
}while(c!=6);
cout<<"\nPress any key to return to main menu";
getch();
}

void modi_rs()                             //To modify Patient's Recovery Status
{
clrscr();
fstream f;
f.open("PATIENT.dat",ios::binary|ios::in|ios::out);
PATIENT p;
int uid;
char nwst[30];
cout<<"Enter Patient's #UID :";
cin>>uid;
while(f.read((char*)&p,sizeof(p)))
{
  if(p.ptuid==uid)
  {
   cout<<"Enter new status: ";
   gets(nwst);
   p.change_status(nwst);
   f.seekp(f.tellg()-sizeof(p));
   f.write((char*)&p,sizeof(p));
   cout<<"Patient's Recovery Status changed\n";
   p.output();
   }
}
cout<<"\nPress any key to return to modify menu";
getch();
}

void modi_ds()                             //To modify Patient's Disease Status
{
clrscr();
fstream f;
f.open("PATIENT.dat",ios::binary|ios::in|ios::out);
PATIENT p;
int uid;
char nwd[30];
cout<<"Enter Patient's #UID :";
cin>>uid;
while(f.read((char*)&p,sizeof(p)))
{
  if(p.ptuid==uid)
  {
   cout<<"Enter new disease: ";
   gets(nwd);
   p.change_disease(nwd);
   f.seekp(f.tellg()-sizeof(p));
   f.write((char*)&p,sizeof(p));
   cout<<"Patient's Disease Status changed\n";
   p.output();
   }
}
cout<<"\nPress any key to return to modify menu";
getch();
}

void modify_menu()                          //Modify Menu
{
int c;
do
{
   clrscr();
   cout<<" MODIFY PATIENT'S:\n";
   cout<<"1.  RECOVERY STATUS\n";
   cout<<"2.  DISEASE STATUS\n";
   cout<<"3.  QUIT\n";
   cout<<"Enter your choice: ";
   cin>>c;
switch(c)
  {
     case 1: modi_rs(); break;
     case 2: modi_ds(); break;
     case 3: break;
     default: cout<<"\nWrong choice";
  }
}while(c!=3);
cout<<"\nPress any key to return to main menu";
getch();
}

void deletion()                            //To delete patient data
{
clrscr();
fstream f1,f2;
f1.open ("PATIENT.dat",ios::binary|ios::in);
f2.open("TEMP.dat",ios::binary|ios::out);
PATIENT p;
int uid;
int flag=0;
cout<<"Enter Patient's #UID : ";
cin>>uid;
while(f1.read((char*)&p,sizeof(p)))
{
 if(p.ptuid!=uid)
   f2.write((char*)&p,sizeof(p));
 else
   flag++;
}
f1.close();
f2.close();
if(flag)
  cout<<"Patient data deleted\n";
else
  cout<<"No Patient found\n";

remove("PATIENT.dat");
rename("TEMP.dat","PATIENT.dat");
cout<<"\nPress any key to return to main menu";
getch();
}

void discharge()                           //To discharge a patient
{
clrscr();
fstream f;
f.open("PATIENT.dat",ios::binary|ios::in|ios::out);
PATIENT p;
int uid,x;
char nwdst[35];
cout<<"DISCHARGED AS\n";
cout<<"1.  Improved and Discharged\n";
cout<<"2.  Not Improved and Discharged\n";
cout<<"3.  LAMA(Left Against Medical Advice)\n";
cout<<"4.  Expired (cause of death)\n";

cout<<"Enter Patient's #UID to be discharged :";
cin>>uid;
while(f.read((char*)&p,sizeof(p)))
{
  if(p.ptuid==uid)
  {
   cout<<"Enter discharge status no. as from menu: ";
   cin>>x;
   switch(x)
      {
       case 1:strcpy(nwdst,"Improved and Discharged");
	      break;
       case 2:strcpy(nwdst,"Not Improved and Discharged");
	      break;
       case 3:strcpy(nwdst,"LAMA(Left Against Medical Advise)");
	      break;
       case 4:strcpy(nwdst,"Expired (cause of death)");
	      break;
      }
   p.change_status(nwdst);
   f.seekp(f.tellg()-sizeof(p));
   f.write((char*)&p,sizeof(p));
   p.roomno=0;
   cout<<"Patient discharged\n\n";
   p.output();
   }
}
cout<<"\nPress any key to return to main menu";
getch();
}

void main()
{
clrscr();
cout<<"******************************\n";
cout<<"*  COMPUTER SCIENCE PROJECT  *\n";
cout<<"*                            *\n";
cout<<"* HOSPITAL MANAGEMENT SYSTEM *\n";
cout<<"*         VERSION 1.O        *\n";
cout<<"*                            *\n";
cout<<"*           LAVANYA RAJ          *\n";
cout<<"*                 21694097               *\n";
cout<<"*               CLASS XII              *\n";
cout<<"*               (2019-2020)             *\n";
cout<<"******************************\n";
getch();
int x;
do
{
clrscr();
cout<<"\n";
cout<<"########################\n";
cout<<"#                      #\n";
cout<<"# MEERUT CITY HOSPITAL #\n";
cout<<"#                      #\n";
cout<<"########################\n\n\n";
cout<<"SERVICES PROVIDED\n";
cout<<"1. List of Departments\n";
cout<<"2. Admit Patient\n";
cout<<"3. Display Patients\n";

