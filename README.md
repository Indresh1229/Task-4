# Task-4
#include <iostream>
#include <vector>
#include <string>

struct Task {
    std::string description;
    bool is_done;
};

class ToDoList {
private:
    std::vector<Task> tasks;

public:
    void addTask(const std::string& taskDescription) {
        Task newTask{taskDescription, false};
        tasks.push_back(newTask);
        std::cout << "Task added: " << taskDescription << std::endl;
    }

    void viewTasks() const {
        if (tasks.empty()) {
            std::cout << "Your to-do list is empty!" << std::endl;
        } else {
            std::cout << "Your to-do list:" << std::endl;
            for (size_t i = 0; i < tasks.size(); ++i) {
                std::cout << i + 1 << ". " << tasks[i].description
                          << " [" << (tasks[i].is_done ? "Done" : "Not Done") << "]" << std::endl;
            }
        }
    }

    void markTaskAsDone(int taskIndex) {
        if (taskIndex < 1 || taskIndex > tasks.size()) {
            std::cout << "Invalid task number!" << std::endl;
        } else {
            tasks[taskIndex - 1].is_done = true;
            std::cout << "Task " << taskIndex << " marked as done!" << std::endl;
        }
    }

    void deleteTask(int taskIndex) {
        if (taskIndex < 1 || taskIndex > tasks.size()) {
            std::cout << "Invalid task number!" << std::endl;
        } else {
            std::cout << "Task deleted: " << tasks[taskIndex - 1].description << std::endl;
            tasks.erase(tasks.begin() + taskIndex - 1);
        }
    }
};

int main() {
    ToDoList todo;
    int choice;

    do {
        std::cout << "\nTo-Do List Menu:\n";
        std::cout << "1. Add Task\n";
        std::cout << "2. View Tasks\n";
        std::cout << "3. Mark Task as Done\n";
        std::cout << "4. Delete Task\n";
        std::cout << "5. Exit\n";
        std::cout << "Enter your choice: ";
        std::cin >> choice;

        switch (choice) {
            case 1: {
                std::cin.ignore(); // Clear the newline character from the input buffer
                std::string taskDescription;
                std::cout << "Enter task description: ";
                std::getline(std::cin, taskDescription);
                todo.addTask(taskDescription);
                break;
            }
            case 2:
                todo.viewTasks();
                break;
            case 3: {
                int taskIndex;
                std::cout << "Enter task number to mark as done: ";
                std::cin >> taskIndex;
                todo.markTaskAsDone(taskIndex);
                break;
            }
            case 4: {
                int taskIndex;
                std::cout << "Enter task number to delete: ";
                std::cin >> taskIndex;
                todo.deleteTask(taskIndex);
                break;
            }
            case 5:
                std::cout << "Exiting program." << std::endl;
                break;
            default:
                std::cout << "Invalid choice! Please try again." << std::endl;
        }
    } while (choice != 5);

    return 0;
}
