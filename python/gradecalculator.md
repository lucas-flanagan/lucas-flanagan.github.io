---
layout: default
---

## Grade Calculator

Author: Lucas Flanagan <br>
Date: Nov 2019 <br>
Description: Calculates final grades and produces a transcript based on user input

      def one_class():
          finalscore1 = 0
          print("Class Details")
          print("***************")
          sub1 = input("Enter subject:")
          sub1 = sub1.lower()
          if sub1 == "math":
              coursenum1 = input("Enter Course No: ")
              coursetitle1 = input("Enter Course Title: ")
              attendance1 = float(input("Enter Attendance(%): "))
              if attendance1 > 100:
                  print("Value should be less than 100")
              attendance_1 = attendance1
              attendance1 *= .20
              examscore1 = float(input("Enter Exam Score: "))
              if examscore1 > 100:
                  print("Value should be less than 100")
              examscore_1 = examscore1
              examscore1 *= .40
              hwscore1 = float(input("Enter HW Score: "))
              if hwscore1 > 100:
                  print("Value should be less than 100")
              hwscore_1 = hwscore1
              hwscore1 *= .40
              finalscore1 = attendance1 + examscore1 + hwscore1
              course_name1 = sub1 + coursenum1

              finalgrade1 = ""
              if finalscore1 >= 80:
                  finalgrade1 = "A"
              elif finalscore1 >= 60 and finalscore1 < 80:
                  finalgrade1 = "B"
              elif finalscore1 < 60:
                  finalgrade1 = "C"
              finalgrade_1 = finalgrade1

          elif sub1 == "cs":
              coursenum1 = input("Enter Course No: ")
              coursetitle1 = input("Enter Course Title: ")
              attendance1 = float(input("Enter Attendance(%): "))
              if attendance1 > 100:
                  print("Value should be less than 100")
              attendance_1 = attendance1
              attendance1 *= .10
              examscore1 = float(input("Enter Exam Score: "))
              if examscore1 > 100:
                  print("Value should be less than 100")
              examscore_1 = examscore1
              examscore1 *= .30
              hwscore1 = float(input("Enter HW Score: "))
              if hwscore1 > 100:
                  print("Value should be less than 100")
              hwscore_1 = hwscore1
              hwscore1 *= .60
              finalscore1 = attendance1 + examscore1 + hwscore1

              course_name1 = sub1 + coursenum1

              finalgrade1 = ""
              if finalscore1 >= 80:
                  finalgrade1 = "A"
              elif finalscore1 >= 60 and finalscore1 < 80:
                  finalgrade1 = "B"
              elif finalscore1 < 60:
                  finalgrade1 = "C"
              finalgrade_1 = finalgrade1

          return finalscore1, course_name1, coursetitle1, attendance_1, hwscore_1, examscore_1, finalgrade_1


      def two_classes():
          finalscore1 = 0
          finalscore2 = 0
          print("Class 1 Details")
          print("***************")
          sub1 = input("Enter subject:")
          sub1 = sub1.lower()
          if sub1 == "math":
              coursenum1 = input("Enter Course No: ")
              coursetitle1 = input("Enter Course Title: ")
              attendance1 = float(input("Enter Attendance(%): "))
              if attendance1 > 100:
                  print("Value should be less than 100")
              attendance_1 = attendance1
              attendance1 *= .20
              examscore1 = float(input("Enter Exam Score: "))
              if examscore1 > 100:
                  print("Value should be less than 100")
              examscore_1 = examscore1
              examscore1 *= .40
              hwscore1 = float(input("Enter HW Score: "))
              if hwscore1 > 100:
                  print("Value should be less than 100")
              hwscore_1 = hwscore1
              hwscore1 *= .40
              finalscore1 = attendance1 + examscore1 + hwscore1
              course_name1 = sub1 + coursenum1

              finalgrade1 = ""
              if finalscore1 >= 80:
                  finalgrade1 = "A"
              elif finalscore1 >= 60 and finalscore1 < 80:
                  finalgrade1 = "B"
              elif finalscore1 < 60:
                  finalgrade1 = "C"
              finalgrade_1 = finalgrade1

          elif sub1 == "cs":
              coursenum1 = input("Enter Course No: ")
              coursetitle1 = input("Enter Course Title: ")
              attendance1 = float(input("Enter Attendance(%): "))
              if attendance1 > 100:
                  print("Value should be less than 100")
              attendance_1 = attendance1
              attendance1 *= .10
              examscore1 = float(input("Enter Exam Score: "))
              if examscore1 > 100:
                  print("Value should be less than 100")
              examscore_1 = examscore1
              examscore1 *= .30
              hwscore2 = float(input("Enter HW Score: "))
              if hwscore1 > 100:
                  print("Value should be less than 100")
              hwscore_1 = hwscore1
              hwscore1 *= .60
              finalscore1 = attendance1 + examscore1 + hwscore1
              course_name1 = sub1 + coursenum1

              finalgrade1 = ""
              if finalscore1 >= 80:
                  finalgrade1 = "A"
              elif finalscore1 >= 60 and finalscore1 < 80:
                  finalgrade1 = "B"
              elif finalscore1 < 60:
                  finalgrade1 = "C"
              finalgrade_1 = finalgrade1

          print("")

          print("Class 2 Details")
          print("***************")
          sub2 = input("Enter subject:")
          sub2 = sub2.lower()
          if sub2 == "math":
              coursenum2 = input("Enter Course No: ")
              coursetitle2 = input("Enter Course Title: ")
              attendance2 = float(input("Enter Attendance(%): "))
              if attendance2 > 100:
                  print("Value should be less than 100")
              attendance_2 = attendance2
              attendance2 *= .20
              examscore2 = float(input("Enter Exam Score: "))
              if examscore2 > 100:
                  print("Value should be less than 100")
              examscore_2 = examscore2
              examscore2 *= .40
              hwscore2 = float(input("Enter HW Score: "))
              if hwscore2 > 100:
                  print("Value should be less than 100")
              hwscore_2 = hwscore2
              hwscore2 *= .40
              finalscore2 = attendance2 + examscore2 + hwscore2
              course_name2 = sub2 + coursenum2

              finalgrade2 = ""
              if finalscore2 >= 80:
                  finalgrade2 = "A"
              elif finalscore2 >= 60 and finalscore2 < 80:
                  finalgrade2 = "B"
              elif finalscore2 < 60:
                  finalgrade2 = "C"
              finalgrade_2 = finalgrade2

          elif sub2 == "cs":
              coursenum2 = input("Enter Course No: ")
              coursetitle2 = input("Enter Course Title: ")
              attendance2 = float(input("Enter Attendance(%): "))
              if attendance2 > 100:
                  print("Value should be less than 100")
              attendance_2 = attendance2
              attendance2 *= .10
              examscore2 = float(input("Enter Exam Score: "))
              if examscore2 > 100:
                  print("Value should be less than 100")
              examscore_2 = examscore2
              examscore2 *= .30
              hwscore2 = float(input("Enter HW Score: "))
              if hwscore2 > 100:
                  print("Value should be less than 100")
              hwscore_2 = hwscore2
              hwscore2 *= .60
              finalscore2 = attendance2 + examscore2 + hwscore2
              course_name2 = sub2 + coursenum2

              finalgrade2 = ""
              if finalscore2 >= 80:
                  finalgrade2 = "A"
              elif finalscore2 >= 60 and finalscore2 < 80:
                  finalgrade2 = "B"
              elif finalscore2 < 60:
                  finalgrade2 = "C"
              finalgrade_2 = finalgrade2

          return finalscore1, finalscore2, course_name1, course_name2, coursetitle1, coursetitle2, attendance_1, attendance_2, hwscore_1, hwscore_2, examscore_1, examscore_2, finalgrade_1, finalgrade_2


      name = input("Enter Name: ")
      number_of_classes = int(input("How many classes are you taking this semester?"))

      if number_of_classes == 1:
          finalscore1, course_name1, coursetitle1, attendance_1, hwscore_1, examscore_1, finalgrade_1 = one_class()

          print("***************")
          print("Name :: %s" % name)
          print("***************")
          print("|  Course  |  Course Title  | Attendance | Homework | Exam | Grade |")
          print("| %s |  %s  |  %d  |   %d   |   %d   |   %s   |" %
                (course_name1, coursetitle1, attendance_1, hwscore_1, examscore_1, finalgrade_1))

      elif number_of_classes == 2:
          finalscore1, finalscore2, class_name1, class_name2, coursetitle1, coursetitle2, attendance_1, attendance_2, hwscore_1, hwscore_2, examscore_1, examscore_2, finalgrade_1, finalgrade_2 = two_classes()
          finalgrade1 = ""
          if finalscore1 >= 80:
              finalgrade1 = "A"
          elif finalscore1 >= 60 and finalscore1 < 80:
              finalgrade1 = "B"
          elif finalscore1 < 60:
              finalgrade1 = "C"
          finalgrade2 = ""
          if finalscore2 >= 80:
              finalgrade2 = "A"
          elif finalscore2 >= 60 and finalscore2 < 80:
              finalgrade2 = "B"
          elif finalscore2 < 60:
              finalgrade2 = "C"
          print("***************")
          print("Name :: %s" % name)
          print("***************")
          print("|  Course  |  Course Title  | Attendance | Homework | Exam | Grade |")
          print("| %s |  %s  |  %d  |   %d   |   %d   |   %s   |" %
                (class_name1, coursetitle1, attendance_1, hwscore_1, examscore_1, finalgrade_1))
          print("| %s |  %s  |  %d  |   %d   |   %d   |   %s   |" %
                (class_name2, coursetitle2, attendance_2, hwscore_2, examscore_2, finalgrade_2))

      else:
          print("Invalid number of courses. (Maximum = 2)")
          
Output:

<img src="gradecalc.png">
