# CS 112 - Data Structures

Fall 2025

## Course Overview

An intermediate programming course focusing on fundamental data structures and algorithms using C++. Students will learn to design, implement, and analyze efficient data structures and algorithms.

This repository contains the course materials built as a Jupyter Book website.

## Topics Covered

- Introduction to C++ (compilation, data types, pointers, arrays)
- Control Structures and Functions
- File I/O and Exception Handling
- Classes and Operator Overloading
- Vectors and Dynamic Arrays
- Generic Containers
- Linked Lists and Dynamic Data Structures
- Algorithm Analysis and Big-O Notation
- Stacks and Queues
- Recursion
- Binary Search Trees (BSTs)
- AVL Trees
- STL set and map containers
- Hash Tables and Sorting Algorithms

## Prerequisites

- Understanding of basic programming concepts

## Programming Language

**C++** - All assignments and projects will be implemented in C++

## Course Structure

The course is organized into weekly modules (Week 0-14) plus a final exam period. Each week includes:

- Student Learning Objectives (SLOs)
- Readings and resources
- Laboratory assignments
- Programming projects
- Periodic tests
- Daily quizzes

## Assessment

| Component              | Weight |
| ---------------------- | ------ |
| Laboratory Assignments | 30%    |
| Programming Projects   | 35%    |
| Tests (4 tests)        | 30%    |
| Class Participation    | 5%     |

### Test Schedule

- Test 1: Weeks 0-2 (Friday)
- Test 2: Weeks 0-5 (Friday)
- Test 3: Weeks 0-9 (Friday)
- Test 4: Weeks 0-12 (Friday)
- Final Exam: Cumulative (during exam period)

## Building the Course Website

This course website is built using Jupyter Book. To build and preview the site locally:

### Prerequisites

- Python 3.7+
- pip

### Installation

```bash
pip install jupyter-book
```

### Building the Book

```bash
# Build the book
jupyter-book build .

# Clean previous builds (if needed)
jupyter-book clean .
```

### Preview the Site

After building, open `_build/html/index.html` in your web browser to preview the site locally.

### Publishing

The site can be published to GitHub Pages or other hosting platforms. See the [Jupyter Book documentation](https://jupyterbook.org/publish/gh-pages.html) for deployment instructions.

## Repository Structure

```
├── content/                 # Course content organized by week
│   ├── week00/             # Week 0: Introduction to C++
│   ├── week01/             # Week 1: Control Structures
│   └── ...                 # Additional weekly content
├── _config.yml             # Jupyter Book configuration
├── _toc.yml               # Table of contents
├── README.md              # This file
└── .gitignore            # Git ignore rules
```

## Getting Help

- Office Hours: [TBA]
- Email: [Instructor Email]
- Course Discussion Forum
- [Calvin University CS Department](https://calvin.edu/academics/departments-programs/computer-science/)

## Contributing

If you find errors or have suggestions for improvements, please:

1. Create an issue describing the problem
2. Fork the repository and make your changes
3. Submit a pull request

---

Fall 2025 - CS 112 Data Structures Course Materials
Last updated: August 7, 2025
