# Web Application development proof

---

- [Web Application development proof](#web-application-development-proof)
  - [Intro](#intro)
    - [User friendly](#user-friendly)
    - [Full-stack](#full-stack)
  - [What is Full stack development?](#what-is-full-stack-development)
  - [What does "full-stack development" encompass in regards to learning outcomes?](#what-does-full-stack-development-encompass-in-regards-to-learning-outcomes)
  - [My achievements](#my-achievements)
    - [Backend achievements](#backend-achievements)
      - [Detailed overview](#detailed-overview)
        - [Menu API](#menu-api)
        - [Table API](#table-api)
    - [Frontend achievements](#frontend-achievements)
      - [Detailed overview](#detailed-overview-1)
  - [Links to repositories](#links-to-repositories)


## Intro

### User friendly

*You apply best practices when creating user interfaces and basic user experience testing and development techniques.*

### Full-stack

*You design and build a full stack application using a commonly accepted front end Javascript framework and back end application implementing relevant communication protocols, persistence of data by usage of ORM and addressing asynchronous communication issues.*

## What is Full stack development?

Full stack development is the process of designing, creating, testing, and deploying a complete web application from start to finish. It involves working with various technologies and tools, including **front-end** web development, **back-end** web development, and database development. And full stack development is a term used to describe a software engineer or developer who works with both the **front** and **back** end of a website or application.

## What does "full-stack development" encompass in regards to learning outcomes?

The learning objectives for full-stack development involve gaining a comprehensive understanding and proficiency in front-end and back-end technologies. This includes mastering front-end languages such as HTML, CSS, and JavaScript, as well as frontend JavaScript frameworks like React, Angular, or Vue.js. On the back-end, it involves acquiring knowledge of server-side programming languages like Python, Java, or Node.js, along with frameworks such as Django, Spring Boot, or Express.js. Proficiency in database management systems, understanding of RESTful APIs, integration of different components, and deployment strategies are also key aspects. The aim is to develop the ability to independently create, deploy, and maintain web applications that seamlessly integrate user interfaces, server-side logic, and data storage, providing a holistic understanding of the full software stack.

## My achievements

I will split my achievements in 2 large sections: [Backend achievements](#backend-achievements) and [Frontend achievements](#frontend-achievements).

### Backend achievements

I have achieved significant milestones in full-stack development, particularly in the backend realm. One of my notable accomplishments was designing a robust architecture utilizing microservices. By adopting a microservice architecture, I successfully break down a monolithic application into smaller, independent services, promoting scalability, flexibility, and maintainability. This architectural design allowed for seamless communication and interaction between various microservices.

In addition to designing the architecture, I implemented cutting-edge containerization technologies such as Docker. Leveraging Docker, I containerized each microservice, ensuring consistent deployment across different environments and enabling efficient scaling and resource utilization. This approach contributed to easier deployment and management of the backend components while maintaining isolation, portability and easy-to-use development environment.

```yaml
# my config file for containerized architecture
version: "3"
services:
    # backend

    menu:
        container_name: menu_api
        build: ./menu
        ports:
            - "5000:5000"
        volumes:
            - ./menu:/usr/src/app
            - /usr/src/app/node_modules
        depends_on:
            - menu_db
        restart: always
        environment:
            DB_URI: "postgresql://root:eatn@menu_db:5432/menu"

    menu_db:
        container_name: menu_db
        image: postgres
        volumes:
            - ./db_volumes/menu/:/var/lib/postgresql/data
        restart: always
        environment:
            POSTGRES_USER: root
            POSTGRES_PASSWORD: eatn
            POSTGRES_DB: menu

    tables:
        container_name: tables_api
        build: ./tables
        ports:
            - "5001:5001"
        volumes:
            - ./tables:/usr/src/app
            - /usr/src/app/node_modules
        depends_on:
            - tables_db
        restart: always
        environment:
            DB_URI: "postgresql://root:eatn@tables_db:5432/tables"

    tables_db:
        container_name: tables_db
        image: postgres
        volumes:
            - ./db_volumes/tables/:/var/lib/postgresql/data
        restart: always
        environment:
            POSTGRES_USER: root
            POSTGRES_PASSWORD: eatn
            POSTGRES_DB: tables

    # reverse proxy

    nginx:
        container_name: eatn_proxy
        image: nginx
        volumes:
            - ./nginx/nginx.conf:/etc/nginx/nginx.conf
        ports:
            - "8000:80"
        depends_on:
            - menu
            - tables
        
        restart: always

    # frontend
    
    cashier_frontend:
        container_name: cashier_frontend
        build: ./cashier_frontend
        ports:
            - "4000:4000"
        volumes:
            - ./cashier_frontend:/usr/src/app
            - /usr/src/app/node_modules
        depends_on:
            - nginx
            - menu
            - tables
        restart: always
        env_file: cashier_frontend/.env

```

To enable effective communication between the frontend and backend, I designed multiple REST APIs using Node.js and the Express.js framework. Following REST principles, I defined clear and intuitive endpoints, adhered to the proper use of HTTP verbs, and established appropriate response formats such as JSON. These APIs facilitated seamless data exchange between the frontend and backend components, enabling efficient client-server interaction.

Furthermore, I designed a relational database using PostgreSQL. By employing proper database modeling techniques, I ensured the database schema represented the application's data accurately and efficiently. I implemented table relationships, defined constraints, and optimized queries to enhance database performance. This design decision allowed for reliable and structured data storage, retrieval, and manipulation, supporting the backend functionality effectively.

In summary, my achievements in the backend realm encompass designing a microservice architecture, implementing containerization using Docker, creating REST APIs with Node.js and Express.js, and designing a relational database using PostgreSQL. These accomplishments demonstrate my expertise in backend development, emphasizing my ability to architect scalable systems, facilitate frontend-backend communication, and ensure efficient data storage and retrieval.

#### Detailed overview

If you want to experience data flow of the APIs, you can do so using provided [Insomnia](https://insomnia.rest/) config files for setting up example requests for each API respectively.

![Insomnia client](../imgs/InsomniaExample.png)

##### Menu API

This service serves as a main data storage/query service as whole project feeds off it. It mainly stores the data for menu items, menu item tags the describe the menu item even further and  hierarchy system which includes categories and corresponding subcategories. 

For each named resource, there is a router/controller which controls the data flow coming in and out of the database.


```
.
├── CategoryRouter.js
├── MenuItemRouter.js
├── SubcategoryRouter.js
└── TagRouter.js
```


##### Table API

This service serves as a service which stores all the tables in the establishment. This is not a real-time guest tracking service, but more of a establishment configuration service.

It has only router which allows for getting table data, creating new tables, updating and deleting existing ones.

### Frontend achievements

I have achieved significant milestones in frontend development, particularly in developing a Single Page Application (SPA) using the cutting-edge web framework SvelteKit. Following a component-driven design approach, I successfully created a highly interactive and performant application. By leveraging SvelteKit's efficient rendering and state management capabilities, I developed reusable and modular components, enabling seamless code organization and maintainability. This achievement showcases my expertise in utilizing modern frontend frameworks and adopting best practices for building engaging and scalable web applications.

#### Detailed overview

My website is a Single Page Application builtin SvelteKit, Javascript framework. Sveltekit is a bleeding-edge frontend framework which takes a new approach to component-based development and DOM rendering by *compiling* custom Javascript code into minified files that can be executed blazingly fast.

![Web example 1](../imgs/webExample1.png)

![Web example 2](../imgs/webExample2.png)


## Links to repositories

- [Menu API (backend)](https://github.com/eatn-dev/eatn_menu_api)
- [Table API (backend)](https://github.com/eatn-dev/eatn_tables_api)
- [Cashier's website (frontend)](https://github.com/eatn-dev/eatn_cashier_frontend)

