#!/bin/bash

tasks_file="tasks.txt"

initialize_tasks_file() {
    touch "$tasks_file"
}

add_task() {
    echo "$1" >> "$tasks_file"
    echo "Task added: $1"
}

list_tasks() {
    echo "Tasks:"
    if [ -s "$tasks_file" ]; then
        cat -n "$tasks_file"
    else
        echo "No tasks found."
    fi
}

remove_task() {
    if [ -s "$tasks_file" ]; then
        if [ -n "$1" ]; then
            sed -i "${1}d" "$tasks_file"
            echo "Task removed."
        else
            echo "Usage: $0 remove <task_number>"
        fi
    else
        echo "No tasks found."
    fi
}

case "$1" in
    add)
        add_task "${*:2}"
        ;;
    list)
        list_tasks
        ;;
    remove)
        remove_task "$2"
        ;;
    *)
        echo "Usage: $0 {add|list|remove}"
        exit 1
        ;;
esac
