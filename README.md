# Load Testing with Apache JMeter

This repository contains an ongoing non-functional testing project focused on designing, executing, and automating **API load tests** using **Apache JMeter**. The goal of this project is to simulate real-world user behavior, analyze system performance under load, and integrate performance tests into a CI pipeline.

---

## 📌 Project Goals

* Simulate concurrent user traffic against public APIs
* Validate system behavior under increasing load
* Capture and analyze key performance metrics
* Automate load tests using CI (GitHub Actions)
* Practice production-like test design and Git workflows

---

## 🗂️ Project Structure

```
load-testing/
├── jmeter/
│   └── login_and_products_test.jmx   # JMeter Test Plan
├── testdata/
│   └── users.csv                     # Test data for CSV-driven login
├── report/                           # Generated JMeter HTML reports (ignored in Git)
├── jmeter.log                        # Local JMeter execution logs

```

---

## 🧪 Test Scenarios

### 1️⃣ Login API Load Test

* Simulates multiple users logging in concurrently
* Uses **CSV Data Set Config** to supply unique credentials
* Validates authentication behavior under load

**Key features:**

* Thread Group with configurable users, ramp-up, and loops
* JSON request body with parameterized username/password
* Header Manager for API content type

---

### 2️⃣ Products API Test

* Executes product retrieval requests
* Can be chained after login to mimic real user flow
* Used to simulate multi-step user journeys

---

## 📊 Test Data Management

* Test users are stored in `testdata/users.csv`
* Each thread reads unique credentials
* CSV configuration ensures:

  * No reuse of credentials once exhausted
  * Threads stop gracefully at EOF

This setup allows **safe concurrent execution** without repeated login failures.

---

## ⚙️ Running Tests Locally

Example command:

```
bash
/path/to/apache-jmeter/bin/jmeter \
  -n \
  -t jmeter/login_and_products_test.jmx \
  -l results.jtl

```

To generate an HTML report:

```
bash
/path/to/apache-jmeter/bin/jmeter \
  -g results.jtl \
  -o report/

```

> ⚠️ Generated reports are intentionally excluded from Git.

---

## 🤖 CI Integration (GitHub Actions)

This project is integrated with **GitHub Actions** to:

* Automatically run JMeter tests on push
* Validate that the test plan executes successfully in CI
* Mimic real-world performance testing pipelines

This ensures performance checks are **repeatable and automated**.

---

## 🌿 Git Workflow

This repo follows a **feature-branch workflow**:

* `main` → stable baseline
* `feature/*` → new test scenarios or improvements
* Changes are developed in feature branches and merged back

This mirrors how performance testing is handled in real teams.

---

## 🚀 Future Enhancements

* Increase load with controlled pacing and throughput shaping
* Add assertions for response time SLAs
* Add trend comparison across runs
* Publish CI artifacts (reports) optionally
* Extend scenarios to full user journeys

---

## 🧠 Learning Outcomes

* Practical JMeter test plan design
* Understanding of concurrency vs data constraints
* CI-driven performance testing
* Clean Git practices for test automation projects

---

📌 *This project is actively evolving as new performance testing concepts are explored.*
