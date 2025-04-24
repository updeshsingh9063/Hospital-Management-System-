##hospital management software @cbsepython.in
##PRINTING WELCOME NOTE while(True): print("""
================================
WELCOME TO MYHOSPITAL
================================
""")
##creating database connectivity import mysql.connector
passwd=str(input("ENTER THE DATABASE PASSWORD;"))
mysql=mysql.connector.connect(host="localhost",user="root",passwd="123456789") mycursor=mysql.cursor() #creating database
mycursor.execute("create database if not exists my_hospitals") mycursor.execute("use my_hospitals") #creating the tables we need
mycursor.execute("create table if not exists patient_details(name varchar(30) not null,age
int(3),address varchar(50),doctor_recommended varchar(30))")
mycursor.execute("create table if not exists doctor_details(name varchar(30) primary
key,specialisation varchar(40),age int(2),address varchar(30),contact varchar(15),fees int(10),monthly_salary int(10))")
mycursor.execute("create table if not exists nurse_details(name varchar(30) primary key,age
int(2),address varchar(30),contact varchar(15),monthly_salary int(10))")
mycursor.execute("create table if not exists other_workers_details(name varchar(30) primary
key,age int(2),address varchar(30),contact varchar(15),monthly_salary int(10))")
#login or signup option
#creating table for storing the username and password of the user
mycursor.execute("create table if not exists user_data(username varchar(30) primary
key,password varchar(30) default'000')")
#printing option while(True): print("""
SIGN IN (LOGIN)
SIGN UP (REGISTER)
""")
r=int(input("enter your choice:"))
#IF USER WANTS TO REGISTER if r==2: print("""
=======================================
!!!!!!!PLEASE REGISTER YOURSELF!!!!!!!!
=======================================
""")
u=input("ENTER YOUR PREFERRED USERNAME!!:")
p=input("ENTER YOUR PREFERRED PASSWORD (PASSWORD SHOULD BE
STRONG!!!:")
#ENTERING THE ENTERED VALUE TO THE USER_DATA TABLE mycursor.execute("insert into user_data values('"+u+"','"+p+"')") mysql.commit()
print("""
=======================================
!!!!!!!!REGISTERED SUCCESSFULLY!!!!!!!!
=======================================
""")
x=input("enter any key to continue:")
#IF USER WANTS TO LOGIN elif r==1:
#PRINTING THE SINGIN OPTION AGAIN TO THE USER AFTER REGISTRATION
print("""
==================================
!!!!!!!! {{SIGN IN }} !!!!!!!!!!
==================================
""")
un=input("ENTER THE USERNAME!!:") ps=input("ENTER THE PASSWORD!!:")
mycursor.execute("select password from user_data where username='"+un+"'") row=mycursor.fetchall() for i in row: a=list(i) if a[0]==str(ps): while(True):
##displaying the task you can perform print("""
1.ADMINISTRATION
2.PATIENT (ADMISSION AND DISCHARGE PROCESS)
3.SIGN OUT
""")
##asking for the task from user a=int(input("ENTER YOUR CHOICE:"))
#if user wants to enter administration option if a==1: print("""
SHOW DETAILS
ADD NEW MEMBER
DELETE EXISTING ONE
EXIT
""")
b=int(input("ENTER YOUR CHOICE:")) #showing the existing details if b==1: print("""
DOCTOR DETAILS
NURSE DETAILS
OTHER WORKERS
""")
#ASKING USER'S CHOICE c=int(input("ENTER YOUR CHOICE:")) #if user wants to see the details of doctors if c==1:
mycursor.execute("select * from doctor_details") row=mycursor.fetchall() for i in row: b=0
v=list(i)
k=["NAME","SPECIALISATION","AGE","ADDRESS","CONTACT","FEES","MONTHLY_SALARY
"] d=dict(zip(k,v)) print(d)
#if user wants to see the details of nurses elif c==2:
mycursor.execute("select * from nurse_details") row=mycursor.fetchall() for i in row: v=list(i)
k=["NAME","SPECIALISATION","AGE","ADDRESS","CONTACT","MONTHLY_SALARY"]
d=dict(zip(k,v)) print(d)
#if user wants to see the details of other_workers elif c==3:
mycursor.execute("select * from other_workers_details") row=mycursor.fetchall() for i in row: v=list(i)
k=["NAME","SPECIALISATION","AGE","ADDRESS","CONTACT","MONTHLY_SALARY"]
d=dict(zip(k,v)) print(d)
#IF USER WANTS TO ENTER DETAILS b==2:
print("""

DOCTOR DETAILS
NURSE DETAILS
OTHER WORKERS
""")
c=int(input("ENTER YOUR CHOICE:")) #FOR ENTERING DETAILS OF DOCTORS if c==1:
#ASKING THE DETAILS name=input("ENTER DR. NAME:") spe=input("ENTER SPECIALISATION:") age=input("ENTER AGE:") add=input("ENTER ADDRESS:") cont=input("ENTER CONTACT NO.:") fees=input("ENTER FEES:") ms=input("ENTER MONTHLY_SALARY:")
#INSERTING VALUES ENTERED INTO THE DOCTORS_TABLE mycursor.execute("insert into doctor_details
values('{}','{}',{},'{}',{},{},{}".format(name,spe,age,add,cont,fees,ms))
mysql.commit() print("SUCCESSFULLY ADDED") #for entering nurse details elif c==2:
#ASKING THE DETAILS name=input("ENTER NURSE NAME:") age=input("ENTER AGE:") add=input("ENTER ADDRESS:") cont=input("ENTER CONTACT NO.:") ms=int(input("ENTER MONTHLY_SALARY:")) #INSERTING VALUES ENTERED TO THE TABLE mycursor.execute("insert into nurse_details
values('{}',{},'{}',{},{}".format(name,age,add,cont,ms)) mysql.commit() print("SUCCESSFULLY ADDED") #for entering workers details elif c==3:
#ASKING THE DETAILS name=input("ENTER WORKER NAME:") age=input("ENTER AGE:") add=input("ENTER ADDRESS:") cont=input("ENTER CONTACT NO.:") ms=input("ENTER MONTHLY_SALARY:")
#INSERTING VALUES ENTERED TO THE TABLE
mycursor.execute("insert into other_workers_details
values('{}',{},'{}',{},{}".format(name,age,add,cont,ms)) mysql.commit() print("SUCCESSFULLY ADDED")
#if unser wants to delete data b==3: print("""
DOCTOR DETAILS
NURSE DETAILS
OTHER WORKERS
""")
c=int(input("ENTER YOUR CHOICE:"))
#deleting doctor's details if c==1:
name=input("ENTER DOCTOR'S NAME:")
mycursor.execute("select * from doctor_details where name=='"+name+"'") row=mycursor.fetchall() print(row)
p=input("you really wanna delete this data? (y/n):") if p=="y":
mycursor.execute("delete from doctor_details where name='"+name+"'") mysql.commit()
print("SUCCESSFULLY DELETED!!") else:
print("NOT DELETED")
#deleting nurse details elif c==2:
name=input("ENTER NURSE NAME:")
mycursor.execute("select * nurse_details where name=='"+name+"'") row=mycursor.fetchall() print(row)
p=input("you really wanna delete this data? (y/n):") if p=="y":
mycursor.execute("delete from nurse_details where name='"+name+"'") mysql.commit()
print("SUCCESSFULLY DELETED!!") else:
print("NOT DELETED") #deleting other_workers details elif c==3:
name=input("ENTER THE WORKER NAME:")
mycursor.execute("select * from workers_details where
name=='"+name+"'") row=mycursor.fetchall() print(row)
p=input("you really wanna delete this data? (y/n):") if p=="y":
mycursor.execute("delete from other_workers_details where
name='"+name+"'") mysql.commit()
print("SUCCESSFULLY DELETED!!") else:
print("NOT DELETED")
b==4: break #entering the patient details table elif a==2: print("""
SHOW PATIENT DETAILS
ADD NEW PATIENT
DISCHARGE PATIENT 4. EXIT
""")
b=int(input("ENTER YOUR CHOICE:"))
#showing the existing details
#if user wants to see the details of PATIENT if b==1:
mycursor.execute("select * from patient_details") row=mycursor.fetchall() for i in row: b=0
v=list(i)
k=["NAME","AGE","ADDRESS","CONTACT"]
d=dict(zip(k,v)) print(d)
#adding new patient elif b==2:
name=str(input("ENTER NAME: ")) age=str(input("ENTER AGE: ")) address=str(input("ADDRESS: ")) contact=str(input("CONTACT NUMBER: ")) mycursor.execute ("insert into patient_details
values('{}',{},'{}',{}".format(name,age,address,contact))
mysql.commit()
mycursor.execute("select * from patient_details") for i in mycursor: v=list(i)
k=['NAME','AGE','ADDRESS','CONTACT'] print(dict(zip(k,v))) print("""
====================================
!!!!!!!REGISTERED SUCCESSFULLY!!!!!!
====================================
""") #dischare process elif b==3: name=input("ENTER THE PATIENT NAME:")
mycursor.execute("select * from patient_details where name='"+name+"'") row=mycursor.fetchall() print(row)
bill=input("HAS HE PAID ALL THE BILLS ? (y/n):") if bill=="y":
mycursor.execute("delete from patient_details where name='"+name+"'")

mysql.commit() #if user wants to exit elif b==4: break
###SIGN OUT elif a==3: break
#IF THE USERNAME AND PASSWORD IS NOT IN THE DATABASE else: break
