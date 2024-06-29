# TODO
#include <iostream>
#include <string>
#include <vector>
#include <climits>

using namespace std;

class Task {
private:
    string description;
    bool isComplete;

public:
    Task(const string& desc) : description(desc), isComplete(false) {}

    void markComplete() {
        isComplete = true;
    }

    void markIncomplete() {
        isComplete = false;
    }

    string getDescription() const {
        return description;
    }

    bool getStatus() const {
        return isComplete;
    }

    void displayTask() const {
        cout << (isComplete ? " ->" : " ") << description << endl;
    }
};

class ToDoList {
private:
    vector<Task> tasks;

public:
    void addTask(const string& desc) {
        tasks.push_back(Task(desc));
        cout << "Your task has been added!" << endl;
    }

    void deleteTask(int index) {
        if (index >= 0 && index < tasks.size()) {
            tasks.erase(tasks.begin() + index);
            cout << "Your task has been deleted!" << endl;
        } else {
            cout << "There is no task to delete." << endl;
        }
    }

    void markTaskComplete(int index) {
        if (index >= 0 && index < tasks.size()) {
            tasks[index].markComplete();
            cout << "Task has been marked as complete!" << endl;
        } else {
            cout << "Invalid entry!" << endl;
        }
    }

    void markTaskIncomplete(int index) {
        if (index >= 0 && index < tasks.size()) {
            tasks[index].markIncomplete();
            cout << "Task has been marked as incomplete!" << endl;
        } else {
            cout << "Invalid entry!" << endl;
        }
    }

    void displayTasks() const {
        for (int i = 0; i < tasks.size(); ++i) {
            cout << i + 1 << ". ";
            tasks[i].displayTask();
        }
    }
};

int main() {
    ToDoList myList;
    int choice;
    string taskDesc;
    int taskIndex;

    while (true) {
        cout << "My To-Do List" << endl;
        cout << "1. Add Task" << endl;
        cout << "2. Delete Task" << endl;
        cout << "3. Mark Task Complete" << endl;
        cout << "4. Mark Task Incomplete" << endl;
        cout << "5. Display Tasks" << endl;
        cout << "6. Exit" << endl;
        cout << "Enter your choice: ";
        cin >> choice;
cout<<endl;
        if (cin.fail()) {
            cin.clear();
            cin.ignore(INT_MAX, '\n');
            cout << "Invalid choice! Please try again." << endl;
            continue;
        }

        cin.ignore(INT_MAX, '\n'); 
        switch (choice) {
            case 1:
                cout << "Enter task description: ";
                getline(cin, taskDesc);
                myList.addTask(taskDesc);
                break;
            case 2:
            case 3:
            case 4:
                cout << "Enter task index: ";
                cin >> taskIndex;
                if (cin.fail()) {
                    cin.clear();
                    cin.ignore(INT_MAX, '\n');
                    cout << "Invalid entry!" << endl;
                } else {
                    switch (choice) {
                        case 2:
                            myList.deleteTask(taskIndex - 1);
                            break;
                        case 3:
                            myList.markTaskComplete(taskIndex - 1);
                            break;
                        case 4:
                            myList.markTaskIncomplete(taskIndex - 1);
                            break;
                    }
                }
                break;
            case 5:
                myList.displayTasks();
                break;
            case 6:
                return 0;
            default:
                cout << "Invalid choice! Please try again." << endl;
        }
    }

    return 0;
}
