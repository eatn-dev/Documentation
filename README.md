# Portfolio

by Ivan Sakal

- [Portfolio](#portfolio)
  - [Introduction](#introduction)
  - [Learning outcomes](#learning-outcomes)
  - [Proof and self assessment](#proof-and-self-assessment)
    - [Web Application](#web-application)
    - [Software Quality](#software-quality)
    - [CI/CD](#cicd)

---

## Introduction

This portfolio will serve as a guide to my individual project for third semester of FHICT (2022-2023). This repository will act as a summary of my work in this semester, along with explanations and evidence of how I fulfilled learning outcomes for this semester.

Grading system is explained [here](https://fhict.instructure.com/courses/12993/outcomes), but I'll go over it briefly. Grading system is based on proficiency rating of different skills which Fontys deems necessary for real-life work. The ratings range like this: 

- Undefined
- Beginning
- Proficient
- Advanced
  
## Learning outcomes

For a detailed list of learning outcomes, see [here](./docs/learning_outcomes/learning_outcomes.md).



## Proof and self assessment

| Learning outcome | proof |
|---|---|
| Web Application | [proof](./docs/proofs/1_web_application.md) |
| Sofware Quality | [proof](./docs/proofs/2_code_quality.md) |
| CI/CD | [proof](./docs/proofs/4_cicd.md) |

### Web Application

<table>
  <tr>
    <th><strong>Learning Outcome</strong></th>
    <td>"You desgin and build user-friendly, full-stack web applications."</td>
  </tr>
  <tr>
    <th><strong>Proficiency Rating</strong></th>
    <td>Advanced</td>
  </tr>
  <tr>
    <th><strong>Explanation</strong></th>
    <td>
        <p>
          In this semester I have managed to set up a full SvelteKit web application together with 2 Node.js APIs with respective databases that sit behind an Nginx proxy.
        </p>
        <p>
          The web application is built with usability and speed in mind, both website performance and development speed. Native Svelte 2-way data binding is used to keep the code tidy and performant
        </p>
        <p>
          The UI is made with Bootstrap, library whose main focus is development speed and device compatibility. The website is developed with mobile users in mind.
        </p>
        <p>
          The whole system runs on Docker containers and they talk to each other using Docker's networks built for inter-container fast paced communication.
        </p>
    </td>
  </tr>
</table>

### Software Quality

<table>
  <tr>
    <th><strong>Learning Outcome</strong></th>
    <td>"You use software tooling and methodology that continuously monitors and improve the software quality during software development."</td>
  </tr>
  <tr>
    <th><strong>Proficiency Rating</strong></th>
    <td>Advanced</td>
  </tr>
  <tr>
    <th><strong>Explanation</strong></th>
    <td>
        <p>
         All important parts of the system are thoroughly tested through unit tests and integrtion tests to ensure maximum code compatibility and reliability. The code style is being constantly enforced by linter and as last step of precaution, Sonar Cloud static analysis is integrated.
        </p>
        <p>
          All automated test have Sonar's code analysis as las part of the CI/CD pipeline. SonarCloud will keep track of the code's coverage as well as any apparent mistakes or unfavorable code smells. SonarCloud will immediately notify the developer whether a bug introduces itself into the code until it gets fixed. 
        </p>
    </td>
  </tr>
</table>

### CI/CD

<table>
  <tr>
    <th><strong>Learning Outcome</strong></th>
    <td>"You design and implement a (semi)automated software release process that matches the needs of the project context."</td>
  </tr>
  <tr>
    <th><strong>Proficiency Rating</strong></th>
    <td>Proficient</td>
  </tr>
  <tr>
    <th><strong>Explanation</strong></th>
    <td>
        <p>
          Github actions are being extensively utilized when any kind of tests or automated procedures must be performed. The pipeline's multi step definition ensures that code is reliable and follows a standardized style.<br>
          Each type of test has its respective isolated environment for clean code execution and assessment.
        </p>
    </td>
  </tr>
</table>

