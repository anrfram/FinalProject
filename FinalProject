/*
    COP3330 Final Project
    Ashley Fram 
*/

import java.io.BufferedReader;
import java.io.File;
import java.io.FileReader;
import java.io.IOException;
import java.util.ArrayList;
import java.util.HashMap;
import java.util.HashSet;
import java.util.Map;
import java.util.Scanner;
import java.util.Set;


public class FinalProject {

    private static Map<Integer, Faculty> faculties = new HashMap<>();
    private static Map<Integer, Student> students = new HashMap<>();
    private static Map<Integer, Lecture> lectures = new HashMap<>();
    private static Map<Integer, Lab> labs = new HashMap<>();

    public static void main(String[] args) {
    Scanner scanner = new Scanner(System.in);
      
    System.out.print("Enter the absolute path of the file: ");
    String filePath = scanner.nextLine();
    File file = new File(filePath);
      
    while (!file.exists()) {
        System.out.println("Sorry no such file or invalid file name.");
        System.out.print("Try again: ");
        filePath = scanner.nextLine();
        file = new File(filePath);
    }
      
    System.out.println("File Found! Let's proceed...");
    System.out.println("*****************************************");

    loadFromFile(filePath);

    int choice = -1;
    // rest of the code


        while (choice != 7) {
            System.out.println("Choose one of these options:");
            System.out.println("1- Add a new Faculty to the schedule");
            System.out.println("2- Enroll a Student to a Lecture");
            System.out.println("3- Print the schedule of a Faculty");
            System.out.println("4- Print the schedule of a TA");
            System.out.println("5- Print the schedule of a Student");
            System.out.println("6- Delete a Lecture");
            System.out.println("7- Exit");

            System.out.print("Enter your choice: ");
            choice = scanner.nextInt();
            scanner.nextLine();

            switch (choice) {
            case 1:
                addFaculty(scanner);
                break;
            case 2:
                enrollStudent(scanner);
                break;
            case 3:
                printFacultySchedule(scanner);
                break;
            case 4:
                printTASchedule(scanner);
                break;
            case 5:
                printStudentSchedule(scanner);
                break;
            case 6:
                deleteLecture(scanner);
                break;
            case 7:
                System.out.println("Bye!");
                break;
            default:
                System.out.println("Invalid choice. Please try again.");
            }

            System.out.println("*****************************************");
        }

        scanner.close();
    }

    private static void loadFromFile(String filePath) {
        try (BufferedReader br = new BufferedReader(new FileReader(filePath))) {
            String line;
            while ((line = br.readLine()) != null) {
                String[] parts = line.split(",");
                int crn = Integer.parseInt(parts[0]);
                String title = parts[1];
                String type = parts[2];
                String location = parts[3];

                if (type.equals("Lecture")) {
                    Lecture lecture = new Lecture(crn, title, location);
                    lectures.put(crn, lecture);
                } else if (type.equals("Lab")) {
                    int parentCrn = Integer.parseInt(parts[4]);
                    Lab lab = new Lab(crn, title, location, parentCrn);
                    labs.put(crn, lab);
                }
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

  // Incorrect digits for id
public static class IdException extends Exception {
    public IdException(String message) {
        super(message);
    }
}



  
  // Choice 1, Add a new Faculty to the schedule

private static void addFaculty(Scanner scanner) {
            System.out.print("Enter UCF id: ");
    int id;
    try {
        id = scanner.nextInt();
        scanner.nextLine();
        if (String.valueOf(id).length() != 7) {
            throw new IdException("Invalid UCF id format. (Ids are 7 digits)");
        }
    } catch (IdException e) {
                System.out.println(e.getMessage());

        return;
    }

    if (faculties.containsKey(id)) {
        System.out.println("Faculty with this id already exists.");
        return;
    }

        System.out.print("Enter name: ");
        String name = scanner.nextLine();

    System.out.print("Enter rank: ");
    String department = scanner.nextLine();


      System.out.print("Enter office location: ");
    String officeLocation = scanner.nextLine();

    System.out.print("Enter how many lectures: ");
    int numLectures = scanner.nextInt();
    scanner.nextLine();

    //List<Lecture> lectures = new ArrayList<>();
    Set<Integer> assignedCrns = new HashSet<>();
    for (int i = 1; i <= numLectures; i++) {
        System.out.print("Enter the CRN of lecture " + i + ": ");
        int crn = scanner.nextInt();
        scanner.nextLine();
// errors begin after this
    }

}




  
  // choice 2, Enroll a Student to a Lecture

private static void enrollStudent(Scanner scanner) {
    System.out.print("Enter UCF id: ");
    int studentId = scanner.nextInt();
    scanner.nextLine();
    if (!students.containsKey(studentId)) {
        System.out.println("Student with this id does not exist.");
        return;
    }
  System.out.println("Record found/name: ");
    System.out.println("Which lecture to enroll in: ");


    System.out.print("Enter CRN of the lecture: ");
    int crn = scanner.nextInt();
    scanner.nextLine();
    if (!lectures.containsKey(crn)) {
        System.out.println("Lecture with this CRN does not exist.");
        return;
    }

    Lecture lecture = lectures.get(crn);
    if (!lecture.hasCapacity()) {
        System.out.println("Sorry, this lecture is full.");
        return;
    }

    Student student = students.get(studentId);
    if (student.isEnrolledIn(crn)) {
        System.out.println("This student is already enrolled in this lecture.");
        return;
    }

    Set<Integer> enrolledLectures = student.getEnrolledLectures();
    for (int enrolledCrn : enrolledLectures) {
        if (lecture.hasTimeConflictWith(lectures.get(enrolledCrn))) {
            System.out.println("Sorry, this student is already enrolled in a lecture at this time.");
            return;
        }
    }

    lecture.enroll(studentId);
    student.enroll(crn);
    System.out.println("Student enrolled successfully.");
}

  // choice 3, Print the schedule of a Faculty

private static void printFacultySchedule(Scanner scanner) {
    System.out.print("Enter the UCF id: ");
    int facultyId = scanner.nextInt();
    scanner.nextLine();
    if (!faculties.containsKey(facultyId)) {
        System.out.println("Faculty with this id does not exist.");
        return;
    }


    Faculty faculty = faculties.get(facultyId);
    System.out.println(faculty.getName() + "is teaching the following lectures:");

    Map<Integer, Lecture> facultySchedule = faculty.getSchedule();
    for (int crn : facultySchedule.keySet()) {
        Lecture lecture = lectures.get(crn);
        System.out.println(lecture);
        Set<Integer> enrolledStudents = lecture.getEnrolledStudents();
        for (int studentId : enrolledStudents) {
            Student student = students.get(studentId);
            System.out.println("\t" + student);
        }
    }
}

  // choice 4, print the schedule of a TA

private static void printTASchedule(Scanner scanner) {
    System.out.print("Enter the UCF id: ");
    int taId = scanner.nextInt();
    scanner.nextLine();
    if (!faculties.containsKey(taId)) {
        System.out.println("No TA with this id.");
        return;
    }

    Faculty ta = faculties.get(taId);
    System.out.println("Schedule for " + ta.getName() + ":");
    Map<Integer, Lecture> taSchedule = ta.getTASchedule();
    for (int crn : taSchedule.keySet()) {
        Lecture lecture = lectures.get(crn);
        System.out.println(lecture);
        Set<Integer> enrolledStudents = lecture.getEnrolledStudents();
        for (int studentId : enrolledStudents) {
            Student student = students.get(studentId);
            System.out.println("\t" + student);
        }
    }
}


  // choice 5, print the schedule of a Student
  
private static void printStudentSchedule(Scanner scanner) {
    System.out.print("Enter the UCF id: ");
    int studentId = scanner.nextInt();
    scanner.nextLine();
    if (!students.containsKey(studentId)) {
        System.out.println("Student with this id does not exist.");
        return;
    }

    Student student = students.get(studentId);
    System.out.println("Record Found: \n" + student.getName());
  System.out.println("Enrolled in the following lectures:");

    Set<Integer> enrolledLectures = student.getEnrolledLectures();
    for (int crn : enrolledLectures) {
        Lecture lecture = lectures.get(crn);
        System.out.println("Lecture " + crn + ": " + lecture.getTitle() + " (" + lecture.getLocation() + ")");
        Set<Integer> enrolledLabs = student.getEnrolledLabsForLecture(crn);
        for (int labCrn : enrolledLabs) {
            Lab lab = labs.get(labCrn);
            System.out.println("\tLab " + labCrn + ": " + lab.getTitle() + " (" + lab.getLocation() + ")");
        }
    }
}

  // choice 6, Delete a Lecture
  
   private static void deleteLecture(Scanner scanner) {
        System.out.print("Enter CRN of the lecture to delete: ");
        int crn = scanner.nextInt();
        scanner.nextLine();

        if (!lectures.containsKey(crn)) {
            System.out.println("Lecture with this CRN does not exist.");
            return;
        }

        Lecture lecture = lectures.get(crn);
        lecture.delete();
        lectures.remove(crn);
        System.out.println("Lecture deleted successfully.");
    }
}


class Faculty {
    private int id;
    private String name;
    private String department;

    public Faculty(int id, String name, String department) {
        this.id = id;
        this.name = name;
        this.department = department;
    }
  // new
   private Map<Integer, Lecture> schedule;

    public Faculty() {
        this.schedule = new HashMap<Integer, Lecture>();
    }
  public Map<Integer, Lecture> getSchedule() {
        return this.schedule;
    }

  // new

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getDepartment() {
        return department;
    }

    public void setDepartment(String department) {
        this.department = department;
    }

 public Map<Integer, Lecture> getTASchedule() {
        Map<Integer, Lecture> taSchedule = new HashMap<>(); // define taSchedule here

    return taSchedule;
}


}



class Student {
    private int id;
    private String name;
    private Set<Integer> enrolledLectures;

    public Student(int id, String name) {
        this.id = id;
        this.name = name;
        this.enrolledLectures = new HashSet<>();
    }

    public int getId() {
        return id;
    }

    public String getName() {
        return name;
    }

    public Set<Integer> getEnrolledLectures() {
        return enrolledLectures;
    }

    public boolean isEnrolledIn(int crn) {
        return enrolledLectures.contains(crn);
    }

    public void enroll(int crn) {
        enrolledLectures.add(crn);
    }

    public void unenroll(int crn) {
        enrolledLectures.remove(crn);
    }

// new
  public Set<Integer> getEnrolledLabsForLecture(int lectureCRN) {
        Set<Integer> enrolledLabs = new HashSet<>();

    return enrolledLabs;
}
  // new

}


  class Lecture {

    private int crn;
    private String title;
    private String location;
    private int capacity;
    private Set<Integer> enrolledStudents;
    private Faculty faculty;

    public Lecture(int crn, String title, String location) {
        this.crn = crn;
        this.title = title;
        this.location = location;
        this.capacity = 50;
        this.enrolledStudents = new HashSet<>();
        this.faculty = null;
    }

    // getters and setters
    public int getCrn() {
        return crn;
    }

    public void setCrn(int crn) {
        this.crn = crn;
    }

    public String getTitle() {
        return title;
    }

    public void setTitle(String title) {
        this.title = title;
    }

    public String getLocation() {
        return location;
    }

    public void setLocation(String location) {
        this.location = location;
    }

    public int getCapacity() {
        return capacity;
    }

    public void setCapacity(int capacity) {
        this.capacity = capacity;
    }

    public Set<Integer> getEnrolledStudents() {
        return enrolledStudents;
    }

    public void setEnrolledStudents(Set<Integer> enrolledStudents) {
        this.enrolledStudents = enrolledStudents;
    }

    public Faculty getFaculty() {
        return faculty;
    }

    public void setFaculty(Faculty faculty) {
        this.faculty = faculty;
    }

    // methods
    public boolean hasCapacity() {
        return enrolledStudents.size() < capacity;
    }

    public boolean hasTimeConflictWith(Lecture otherLecture) {
        // check for time conflict between this lecture and another lecture
        // return true if there is a time conflict, false otherwise
      return true;
    }

    public void enroll(int studentId) {
        enrolledStudents.add(studentId);
    }

    public void drop(int studentId) {
        enrolledStudents.remove(studentId);
    }

   // public String toString() {
        // return a string representation of the lecture
        // example: "CRN: 12345, Title: Intro to Computer Science, Location: Classroom A"
     // return toString;
   // }
// new
    public void delete() {
  // new
}


}
class Lab {
    private int crn;
    private String title;
    private String location;
    private int parentCrn;

    public Lab(int crn, String title, String location, int parentCrn) {
        this.crn = crn;
        this.title = title;
        this.location = location;
        this.parentCrn = parentCrn;
    }

    public int getCrn() {
        return crn;
    }

    public String getTitle() {
        return title;
    }

    public String getLocation() {
        return location;
    }

    public int getParentCrn() {
        return parentCrn;
    }

    @Override
    public String toString() {
        return "Lab [CRN=" + crn + ", title=" + title + ", location=" + location + ", parent CRN=" + parentCrn + "]";
    }
}

