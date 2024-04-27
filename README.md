# moodswing
```java
import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;
import java.util.Scanner;

class User {
    private String username;
    private String mood;

    public User(String username) {
        this.username = username;
    }

    public String getUsername() {
        return username;
    }

    public String getMood() {
        return mood;
    }

    public void setMood(String mood) {
        this.mood = mood;
    }
}

class Moodswing {
    private List<User> users;
    private Map<String, List<User>> moods;

    public Moodswing() {
        users = new ArrayList<>();
        moods = new HashMap<>();
    }

    public void addUser(User user) {
        users.add(user);
        System.out.println("User " + user.getUsername() + " has joined Moodswing.");
    }

    public void setUserMood(User user, String mood) {
        user.setMood(mood);
        if (!moods.containsKey(mood)) {
            moods.put(mood, new ArrayList<>());
        }
        moods.get(mood).add(user);
        System.out.println(user.getUsername() + " is now feeling " + user.getMood());
    }

    public List<User> getUsersByMood(String mood) {
        return moods.getOrDefault(mood, new ArrayList<>());
    }
}

public class MoodswingApp {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        Moodswing moodswing = new Moodswing();

        System.out.println("Welcome to Moodswing!");

        while (true) {
            System.out.println("\nMenu:");
            System.out.println("1. Create user");
            System.out.println("2. Set user mood");
            System.out.println("3. Get users by mood");
            System.out.println("4. Exit");
            System.out.print("Enter your choice: ");
            int choice = scanner.nextInt();

            switch (choice) {
                case 1:
                    System.out.print("Enter username: ");
                    String username = scanner.next();
                    User newUser = new User(username);
                    moodswing.addUser(newUser);
                    break;
                case 2:
                    System.out.print("Enter username: ");
                    String name = scanner.next();
                    User user = getUserByName(name, moodswing);
                    if (user == null) {
                        System.out.println("User not found!");
                        break;
                    }
                    System.out.print("Enter mood: ");
                    String mood = scanner.next();
                    moodswing.setUserMood(user, mood);
                    break;
                case 3:
                    System.out.print("Enter mood to search for: ");
                    String searchMood = scanner.next();
                    List<User> usersByMood = moodswing.getUsersByMood(searchMood);
                    System.out.println("Users feeling " + searchMood + ":");
                    for (User u : usersByMood) {
                        System.out.println(u.getUsername());
                    }
                    break;
                case 4:
                    System.out.println("Goodbye!");
                    System.exit(0);
                default:
                    System.out.println("Invalid choice. Please try again.");
                    break;
            }
        }
    }

    private static User getUserByName(String username, Moodswing moodswing) {
        for (User user : moodswing.getUsersByMood("")) {
            if (user.getUsername().equals(username)) {
                return user;
            }
        }
        return null;
    }
}
```

This code implements the basic functionality of Moodswing social media. Users can create accounts, set their moods, and search for other users based on their moods. The program runs as a console application, with a simple menu system for user interaction.
