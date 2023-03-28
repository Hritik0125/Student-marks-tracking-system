# Student-marks-tracking-system

import mysql.connector
db = mysql.connector.connect(host = 'localhost', database = 'smts', user = 'root', passwd = 'India@007')    
c = db.cursor()
class college:
    class student:
        def registration():
            ROLL_NO=input("Enter roll no : ")
            PASS_WD=input("Enter password : ")
            smts="insert into student(ROLL_NO,PASS_WD) values({},'{}')".format(ROLL_NO,PASS_WD)
            print(smts)
            c.execute(smts)
            db.commit()
            c.close()
            db.close()
     
    class teacher:
        def enter_marks():
            ROLL_NO=input("Enter roll no : ")
            ENG=input("Enter marks of English : ")
            MATHS=input("Enter marks of maths : ")
            MAR=input("Enter marks of marathi : ")
            HIN=input("Enter marks of hindi : ")

            sky="insert into teacher(ROLL_NO,ENG,MATHS,MAR,HIN) values ({},{},{},{},{})".format(ROLL_NO,ENG,MATHS,MAR,HIN)
            print(sky)
            c.execute(sky)
            db.commit()
            c.close()
            db.close()
            
    class result:
        def display_marks():
            TOT_MARKS=0
            PER_MARKS=0
            ROLL_NO=input("Enter the roll no : ")
            PASS_WD=input("Enter the password : ")

            blow="select * from teacher where ROLL_NO=(select ROLL_NO from student where ROLL_NO={} and PASS_WD='{}')".format(ROLL_NO,PASS_WD)
            c.execute(blow)
            output=c.fetchall()
            print("__________________________")
            print("\nROLL NO : {}".format(ROLL_NO))
            print("__________________________")
            for i in output:
                TOT_MARKS=TOT_MARKS+i[1]+i[2]+i[3]+i[4]
                PER_MARKS=((PER_MARKS+i[1]+i[2]+i[3]+i[4])/400)*100
                print("""
                      \rENGLISH = {}
                      \rMATHS = {}
                      \rMARATHI = {}
                      \rHINDI = {}""".format(i[1],i[2],i[3],i[4]))
            print("__________________________")
            print("TOTAL MARKS OBTAINED : {}".format(TOT_MARKS))
            print("OUT OF MARKS : {}".format(i[5]))
            print(f"\nPERCENTAGE OBTAINED : {PER_MARKS} %")
            c.close()
            
    class resultsave:
        def download():
            TOT_MARKS=0
            PER_MARKS=0
            ROLL_NO=input("Enter the roll no : ")
            PASS_WD=input("Enter the password : ")

            blow="select * from teacher where ROLL_NO=(select ROLL_NO from student where ROLL_NO={} and PASS_WD='{}')".format(ROLL_NO,PASS_WD)
            c.execute(blow)
            output=c.fetchall()
            for i in output:
                TOT_MARKS=TOT_MARKS+i[1]+i[2]+i[3]+i[4]
                PER_MARKS=((PER_MARKS+i[1]+i[2]+i[3]+i[4])/400)*100
                
            file = open(r"C:\Users\SNP\Downloads\Python SIMS\SMTS\result.txt", "x")
            file.write(f"""\r_____________________
                           \rROLL NO : {ROLL_NO}
                           \r_____________________
                           \rENGLISH = {i[1]}
                           \rMATHS   = {i[2]}
                           \rMARATHI = {i[3]}
                           \rHINDI   = {i[4]}
                           \r_____________________
                           \rTOTAL : {TOT_MARKS}
                           \rOUT OFF : {i[5]}
                           \rPERCENTAGE : {PER_MARKS} %
                        """)
            file.close()
            c.close()
