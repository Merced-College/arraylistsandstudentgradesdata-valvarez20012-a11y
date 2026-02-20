/*
 * Name: John Chiero, Nanak Barring, Victor Alvarez
 * Date: 02/19/2026
 * Program: Course Grades Analyzer - reads CSV grade totals and analyzes A percentages.
 */
import java.io.File;
import java.io.FileNotFoundException;
import java.util.ArrayList;
import java.util.Scanner;

public class Main {

    public static void main(String[] args) {

        ArrayList<Course> courses = new ArrayList<>();
        String filename = "courseAndGradesData.csv";

        try (Scanner fileScanner = new Scanner(new File(filename))) {

            if (fileScanner.hasNextLine()) fileScanner.nextLine(); 
            if (fileScanner.hasNextLine()) fileScanner.nextLine(); 

            while (fileScanner.hasNextLine()) {
                String line = fileScanner.nextLine().trim();
                if (line.isEmpty()) continue;

                String[] parts = line.split(",");
                if (parts.length < 6) continue;

                String courseName = parts[0].trim();

                ArrayList<Integer> grades = new ArrayList<>();
                for (int i = 1; i <= 5; i++) {
                    grades.add(Integer.parseInt(parts[i].trim()));
                }

                Course course = new Course(courseName, grades);
                courses.add(course);
            }

        } catch (FileNotFoundException e) {
            System.out.println("File not found: " + filename);
            return;
        } catch (NumberFormatException e) {
            System.out.println("CSV format error: expected numbers for A-F counts.");
            return;
        }

        printSummaryTable(courses);

        Course best = findHighestA(courses);
        if (best != null) {
            printBestCourse(best);
        }

        runSearch(courses);
    }

    private static void printSummaryTable(ArrayList<Course> courses) {
        System.out.printf("%-10s %6s %6s %6s %6s %6s %8s %8s%n",
                "Course", "A", "B", "C", "D", "F", "Total", "A%");
        for (Course c : courses) {
            ArrayList<Integer> g = c.getCourseGrades();
            System.out.printf("%-10s %6d %6d %6d %6d %6d %8d %8.2f%n",
                    c.getCourseName(),
                    g.get(0), g.get(1), g.get(2), g.get(3), g.get(4),
                    c.getTotalGrades(),
                    c.getAPercent());
        }
    }

    private static Course findHighestA(ArrayList<Course> courses) {
        if (courses.isEmpty()) return null;

        Course best = courses.get(0);
        for (Course c : courses) {
            if (c.getAPercent() > best.getAPercent()) {
                best = c;
            }
        }
        return best;
    }

    private static void printBestCourse(Course best) {
        ArrayList<Integer> g = best.getCourseGrades();
        System.out.println();
        System.out.println("Course with highest A%:");
        System.out.println("Course: " + best.getCourseName());
        System.out.printf("A%%: %.2f%n", best.getAPercent());
        System.out.println("Total: " + best.getTotalGrades());
        System.out.println("A,B,C,D,F: " + g.get(0) + "," + g.get(1) + "," + g.get(2) + "," + g.get(3) + "," + g.get(4));
        System.out.println();
    }

    private static void runSearch(ArrayList<Course> courses) {
        Scanner input = new Scanner(System.in);

        System.out.print("Enter a course name to search (example: ACTG-31): ");
        String target = input.nextLine().trim();

        Course found = null;
        for (Course c : courses) {
            if (c.getCourseName().equalsIgnoreCase(target)) {
                found = c;
                break;
            }
        }

        if (found == null) {
            System.out.println("Course not found: " + target);
        } else {
            ArrayList<Integer> g = found.getCourseGrades();
            System.out.println("Found course: " + found.getCourseName());
            System.out.println("A,B,C,D,F: " + g.get(0) + "," + g.get(1) + "," + g.get(2) + "," + g.get(3) + "," + g.get(4));
            System.out.println("Total: " + found.getTotalGrades());
            System.out.printf("A%%: %.2f%n", found.getAPercent());
        }
    }
}