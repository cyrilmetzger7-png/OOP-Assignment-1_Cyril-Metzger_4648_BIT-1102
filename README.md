# Vaccination Tracker

A lightweight, open-source, privacy-respecting Python program for recording vaccine doses and monitoring vaccination coverage.

Built for **PROG211 – Object-Oriented Programming 1**
Department of Information and Communication Technology, Limkokwing University of Creative Technology, Sierra Leone
Assignment: *Real-World Solutions under DPG Standards* (Individual Assignment, 10%)

**Author:** [Your Name] | **Student ID:** [Your ID]
**Examiner:** Amandus Benjamin Coker

---

## Table of Contents

1. [Overview](#overview)
2. [The Problem](#the-problem)
3. [Features](#features)
4. [Project Structure](#project-structure)
5. [Requirements and Installation](#requirements-and-installation)
6. [Usage](#usage)
7. [Sample Output](#sample-output)
8. [OOP Concepts Demonstrated](#oop-concepts-demonstrated)
9. [Digital Public Goods (DPG) Compliance](#digital-public-goods-dpg-compliance)
10. [Testing](#testing)
11. [Limitations and Future Work](#limitations-and-future-work)
12. [Contributing](#contributing)
13. [License](#license)

---

## Overview

The Vaccination Tracker helps health workers record doses given to people and see how many have completed a vaccine schedule. It belongs to the **Health** domain and uses Object-Oriented Programming to model vaccines, recipients and a clinic register.

No names, phone numbers, addresses or national ID numbers are stored. Each person is represented only by an anonymous code (for example `R-0001`), a broad age group and a district.

## The Problem

In many low-resource settings, paper vaccination registers are lost or damaged, multi-dose schedules are hard to follow, and district offices struggle to compile accurate coverage figures. Many digital tools also collect sensitive personal data, which creates privacy risks. This project shows that a simple, free tool can support immunisation work while collecting the minimum data needed.

## Features

- Create vaccine types with the number of doses required
- Register anonymous recipients with an auto-generated ID
- Record doses and block over-dosing beyond the schedule
- Update a recipient's age group or district
- Store all records in a single dictionary keyed by ID, rejecting duplicates
- Display all records in a readable format
- Generate a coverage report (fully vaccinated count and percentage)
- Runs offline with no external libraries

## Project Structure

```
vaccination-tracker/
├── vaccination_tracker.py   # Vaccine, Recipient and VaccinationTracker classes
├── main.py                  # Demonstration of the program
├── tests/                   # Test cases (optional / future)
├── README.md                # Project documentation
└── LICENSE                  # MIT License
```

If you keep everything in a single file, run that file directly. The program works the same way.

| Class | Responsibility |
|---|---|
| `Vaccine` | Describes a vaccine (ID, name, doses required) and counts total vaccines created |
| `Recipient` | An anonymised person with an age group, district and dose history |
| `VaccinationTracker` | A register that stores recipients in one dictionary and produces reports |

## Requirements and Installation

- Python 3.8 or later
- No third-party packages

```bash
# 1. Clone the repository
git clone https://github.com/<your-username>/vaccination-tracker.git

# 2. Move into the folder
cd vaccination-tracker

# 3. Check Python is installed
python --version
```

## Usage

Run the demonstration:

```bash
python main.py
```

Use the classes in your own code:

```python
from vaccination_tracker import Vaccine, Recipient, VaccinationTracker

measles = Vaccine("V01", "Measles", 2)
tracker = VaccinationTracker("My Health Post")

tracker.add_recipient(Recipient.from_sequence(1, "0-4", "Bo"))
tracker.recipients["R-0001"].record_dose(measles)

tracker.display_all()
tracker.coverage_report(measles)
```

Valid age groups: `0-4`, `5-17`, `18-49`, `50+`.

## Sample Output

```text
[V01] Measles - doses required: 2
[V02] Polio - doses required: 3
Vaccines registered: 2
R-0001: already completed Measles.

--- Register: Freetown Community Health Post ---
R-0001 | Age group: 0-4 | District: Western Area Urban | Doses: {'V01': 2}
R-0002 | Age group: 5-17 | District: Western Area Rural | Doses: {'V01': 1}
R-0003 | Age group: 18-49 | District: Kenema | Doses: {}

Coverage for Measles: 1/3 fully vaccinated (33.3%)
```

## OOP Concepts Demonstrated

**Task 1 – Classes and objects.** Three classes with attributes and methods (`update_record()`, `display_info()`). Objects interact when `Recipient.record_dose()` uses a `Vaccine` object, and when the tracker stores `Recipient` objects.

**Task 2 – One data structure.** A single **dictionary** (`self.recipients`) stores all recipients using their unique ID as the key. `add_recipient()` and `display_all()` add and display records.

**Task 3 – Method types.**

| Type | Examples |
|---|---|
| Instance methods | `record_dose()`, `update_record()`, `is_fully_vaccinated()`, `display_info()` |
| Class methods | `Vaccine.get_total_vaccines()`, `Recipient.from_sequence()` |
| Static methods | `Recipient.generate_anonymous_id()`, `Recipient.is_valid_age_group()` |

## Digital Public Goods (DPG) Compliance

| Principle | How this project meets it |
|---|---|
| **Open-source** | Published on GitHub under the MIT License; uses only the Python standard library |
| **Inclusive and accessible** | Works offline on low-spec computers; plain-language messages; broad age groups; clear docstrings for new learners |
| **Privacy-respecting** | No names, addresses, phone numbers or ID numbers; only anonymous ID, age group and district (data minimisation) |
| **Modular and reusable** | Single-responsibility classes that can be imported or adapted, for example for livestock vaccination |

## Testing

Manual test cases performed by running `main()`:

| Test | Expected result |
|---|---|
| Create vaccines and recipients | Objects created, vaccine counter correct |
| Record two doses for one recipient | Dose count becomes 2 |
| Record a third dose of a 2-dose vaccine | Rejected with a message |
| Add a duplicate ID | Rejected with a message |
| Invalid age group | `ValueError` raised |
| Update a district | Record updated |
| Coverage report | Correct percentage shown |

## Limitations and Future Work

- Data is stored in memory only and is lost when the program closes
- Planned: save to an encrypted file or SQLite, a menu-driven or web interface, next-dose reminders, reports by district and age group, local-language support (Krio, Mende, Temne), and automated `unittest` tests

## Contributing

Contributions are welcome: bug fixes, translations, tests and documentation. Please follow these rules:

1. Fork the repository and create a feature branch
2. Write clear commit messages and add docstrings
3. **Never add fields that store personally identifying information**
4. Open a pull request describing your change

## License

This project is released under the [MIT License](LICENSE). You are free to use, copy, modify and share it.

---

*Prepared for PROG211 – Object-Oriented Programming 1, Semester 03 (September 2026 – February 2027).*
