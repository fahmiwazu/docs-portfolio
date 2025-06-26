# :material-database: Salon Appointment Scheduler

## Introduction
In the Build a Salon Appointment Scheduler project, I'll create a database to manage client appointments for a salon. I'll design tables, set up relationships, and write queries to schedule and track appointments, enhancing my SQL skills while building a functional scheduling system.

## Role
- SQL Developer

## Goals

- **Design a Database Schema**: Create tables to store data about clients, appointments, and salon staff.
- **Establish Relationships**: Link tables to associate clients with their appointments and staff with scheduled services.
- **Implement CRUD Operations**: Use SQL to create, read, update, and delete appointment records.
- **Write Queries for Scheduling**: Write SQL queries to manage and view upcoming appointments, staff availability, and client schedules.
- **Create a User-Friendly Interface**: Build a simple interface for salon staff to manage bookings and clients to check availability.
- **Enhance SQL and Backend Skills**: Practice backend development by working with databases and handling real-world scheduling data.

## Resource Overview

??? abstract "Project Directory"
    === "Bash Appointment Service"
        ``` Bash title="salon.sh"
        #!/bin/bash

        PSQL="psql -X --username=freecodecamp --dbname=salon --tuples-only -c"


        echo -e "\n~~~~~ WAZZALON ~~~~~\n"

        echo -e "Welcome to Wazzalon, how can I help you?" 

        MAIN_MENU(){
        # feedback catcher
        if [[ $1 ]]
        then
            echo -e "\n$1"
        fi

        # display available services
        AVAILABLE_SERVICES=$($PSQL "SELECT service_id, name FROM services ORDER BY service_id;")
        
        # check if service are  available
        if [[ -z $AVAILABLE_SERVICES ]]
        then
            echo "Sorry, we dont have any service availabe right now"
        else
            # display service by service id
            echo "$AVAILABLE_SERVICES" | while read SERVICE_ID BAR NAME
            do
            echo "$SERVICE_ID) $NAME" 
            done
            
            # input service
            read SERVICE_ID_SELECTED
            if [[ ! $SERVICE_ID_SELECTED =~ ^[1-5]+$ ]]
            then
            MAIN_MENU "That's not a number"
            else
            # select service id from input
            SERV_AVAIL=$($PSQL "SELECT service_id FROM services WHERE service_id='$SERVICE_ID_SELECTED'")
            # display service name
            NAME_SERV=$($PSQL "SELECT name FROM services WHERE service_id='$SERVICE_ID_SELECTED'")
            
            if [[ -z $SERV_AVAIL ]]
            then
                MAIN_MENU "I could not find that service. What would you like today?"
            else
                echo -e "\nWhat's your phone number?"
                #select phone number
                read CUSTOMER_PHONE

                # check customer name from customers 
                CUSTOMER_NAME=$($PSQL "SELECT name FROM customers WHERE phone='$CUSTOMER_PHONE'")

                # if name not available, create new name
                if [[ -z $CUSTOMER_NAME ]]
                then
                echo -e "\nI don't have a record for that phone number, what's your name?"
                read CUSTOMER_NAME

                # insert new customer into database
                INSERT_NEW_CUSTOMER=$($PSQL "INSERT INTO customers(name, phone) VALUES('$CUSTOMER_NAME','$CUSTOMER_PHONE')")

                fi

                echo -e "\nWhat time would you like your $NAME_SERV, $CUSTOMER_NAME?"
                read SERVICE_TIME
                
                # select customer_id for booking appointment
                CUSTOMER_ID=$($PSQL "SELECT customer_id FROM customers WHERE phone='$CUSTOMER_PHONE'")
                
                # booking appointment 
                INSERT_SERV_RESULT=$($PSQL "INSERT INTO appointments(customer_id, service_id, time) VALUES('$CUSTOMER_ID','$SERVICE_ID_SELECTED','$SERVICE_TIME')")
                
                # print booking accepted
                echo -e "\nI have put you down for a $NAME_SERV at $SERVICE_TIME, $(echo $CUSTOMER_NAME | sed -r 's/^ *| *$//g')."



            fi 
            fi
        fi

        }


        MAIN_MENU
        ```
    === "PosgreSQL Database Dump"
        ``` SQL title="salon.sql"
        --
        -- PostgreSQL database dump
        --

        -- Dumped from database version 12.17 (Ubuntu 12.17-1.pgdg22.04+1)
        -- Dumped by pg_dump version 12.17 (Ubuntu 12.17-1.pgdg22.04+1)

        SET statement_timeout = 0;
        SET lock_timeout = 0;
        SET idle_in_transaction_session_timeout = 0;
        SET client_encoding = 'UTF8';
        SET standard_conforming_strings = on;
        SELECT pg_catalog.set_config('search_path', '', false);
        SET check_function_bodies = false;
        SET xmloption = content;
        SET client_min_messages = warning;
        SET row_security = off;

        DROP DATABASE salon;
        --
        -- Name: salon; Type: DATABASE; Schema: -; Owner: freecodecamp
        --

        CREATE DATABASE salon WITH TEMPLATE = template0 ENCODING = 'UTF8' LC_COLLATE = 'C.UTF-8' LC_CTYPE = 'C.UTF-8';


        ALTER DATABASE salon OWNER TO freecodecamp;

        \connect salon

        SET statement_timeout = 0;
        SET lock_timeout = 0;
        SET idle_in_transaction_session_timeout = 0;
        SET client_encoding = 'UTF8';
        SET standard_conforming_strings = on;
        SELECT pg_catalog.set_config('search_path', '', false);
        SET check_function_bodies = false;
        SET xmloption = content;
        SET client_min_messages = warning;
        SET row_security = off;

        SET default_tablespace = '';

        SET default_table_access_method = heap;

        --
        -- Name: appointments; Type: TABLE; Schema: public; Owner: freecodecamp
        --

        CREATE TABLE public.appointments (
            appointment_id integer NOT NULL,
            customer_id integer,
            service_id integer,
            "time" character varying(255)
        );


        ALTER TABLE public.appointments OWNER TO freecodecamp;

        --
        -- Name: appointments_appointment_id_seq; Type: SEQUENCE; Schema: public; Owner: freecodecamp
        --

        CREATE SEQUENCE public.appointments_appointment_id_seq
            AS integer
            START WITH 1
            INCREMENT BY 1
            NO MINVALUE
            NO MAXVALUE
            CACHE 1;


        ALTER TABLE public.appointments_appointment_id_seq OWNER TO freecodecamp;

        --
        -- Name: appointments_appointment_id_seq; Type: SEQUENCE OWNED BY; Schema: public; Owner: freecodecamp
        --

        ALTER SEQUENCE public.appointments_appointment_id_seq OWNED BY public.appointments.appointment_id;


        --
        -- Name: customers; Type: TABLE; Schema: public; Owner: freecodecamp
        --

        CREATE TABLE public.customers (
            customer_id integer NOT NULL,
            phone character varying(255) NOT NULL,
            name character varying(255) NOT NULL
        );


        ALTER TABLE public.customers OWNER TO freecodecamp;

        --
        -- Name: customers_customer_id_seq; Type: SEQUENCE; Schema: public; Owner: freecodecamp
        --

        CREATE SEQUENCE public.customers_customer_id_seq
            AS integer
            START WITH 1
            INCREMENT BY 1
            NO MINVALUE
            NO MAXVALUE
            CACHE 1;


        ALTER TABLE public.customers_customer_id_seq OWNER TO freecodecamp;

        --
        -- Name: customers_customer_id_seq; Type: SEQUENCE OWNED BY; Schema: public; Owner: freecodecamp
        --

        ALTER SEQUENCE public.customers_customer_id_seq OWNED BY public.customers.customer_id;


        --
        -- Name: services; Type: TABLE; Schema: public; Owner: freecodecamp
        --

        CREATE TABLE public.services (
            service_id integer NOT NULL,
            name character varying(255) NOT NULL
        );


        ALTER TABLE public.services OWNER TO freecodecamp;

        --
        -- Name: services_service_id_seq; Type: SEQUENCE; Schema: public; Owner: freecodecamp
        --

        CREATE SEQUENCE public.services_service_id_seq
            AS integer
            START WITH 1
            INCREMENT BY 1
            NO MINVALUE
            NO MAXVALUE
            CACHE 1;


        ALTER TABLE public.services_service_id_seq OWNER TO freecodecamp;

        --
        -- Name: services_service_id_seq; Type: SEQUENCE OWNED BY; Schema: public; Owner: freecodecamp
        --

        ALTER SEQUENCE public.services_service_id_seq OWNED BY public.services.service_id;


        --
        -- Name: appointments appointment_id; Type: DEFAULT; Schema: public; Owner: freecodecamp
        --

        ALTER TABLE ONLY public.appointments ALTER COLUMN appointment_id SET DEFAULT nextval('public.appointments_appointment_id_seq'::regclass);


        --
        -- Name: customers customer_id; Type: DEFAULT; Schema: public; Owner: freecodecamp
        --

        ALTER TABLE ONLY public.customers ALTER COLUMN customer_id SET DEFAULT nextval('public.customers_customer_id_seq'::regclass);


        --
        -- Name: services service_id; Type: DEFAULT; Schema: public; Owner: freecodecamp
        --

        ALTER TABLE ONLY public.services ALTER COLUMN service_id SET DEFAULT nextval('public.services_service_id_seq'::regclass);


        --
        -- Data for Name: appointments; Type: TABLE DATA; Schema: public; Owner: freecodecamp
        --

        INSERT INTO public.appointments VALUES (73, 113, 5, '1AM');
        INSERT INTO public.appointments VALUES (74, 113, 4, '2AM');
        INSERT INTO public.appointments VALUES (75, 113, 2, '3AM');
        INSERT INTO public.appointments VALUES (76, 114, 4, '5AM');


        --
        -- Data for Name: customers; Type: TABLE DATA; Schema: public; Owner: freecodecamp
        --

        INSERT INTO public.customers VALUES (113, '1234', 'waz');
        INSERT INTO public.customers VALUES (114, '4321', 'Cal');


        --
        -- Data for Name: services; Type: TABLE DATA; Schema: public; Owner: freecodecamp
        --

        INSERT INTO public.services VALUES (1, 'Potong Rambut');
        INSERT INTO public.services VALUES (2, 'Cukur Jenggot');
        INSERT INTO public.services VALUES (3, 'Cabut Bulu Hidung');
        INSERT INTO public.services VALUES (4, 'Cabut Bulu Kaki');
        INSERT INTO public.services VALUES (5, 'Congcong Threatment');


        --
        -- Name: appointments_appointment_id_seq; Type: SEQUENCE SET; Schema: public; Owner: freecodecamp
        --

        SELECT pg_catalog.setval('public.appointments_appointment_id_seq', 76, true);


        --
        -- Name: customers_customer_id_seq; Type: SEQUENCE SET; Schema: public; Owner: freecodecamp
        --

        SELECT pg_catalog.setval('public.customers_customer_id_seq', 114, true);


        --
        -- Name: services_service_id_seq; Type: SEQUENCE SET; Schema: public; Owner: freecodecamp
        --

        SELECT pg_catalog.setval('public.services_service_id_seq', 5, true);


        --
        -- Name: appointments appointments_pkey; Type: CONSTRAINT; Schema: public; Owner: freecodecamp
        --

        ALTER TABLE ONLY public.appointments
            ADD CONSTRAINT appointments_pkey PRIMARY KEY (appointment_id);


        --
        -- Name: customers customers_phone_key; Type: CONSTRAINT; Schema: public; Owner: freecodecamp
        --

        ALTER TABLE ONLY public.customers
            ADD CONSTRAINT customers_phone_key UNIQUE (phone);


        --
        -- Name: customers customers_pkey; Type: CONSTRAINT; Schema: public; Owner: freecodecamp
        --

        ALTER TABLE ONLY public.customers
            ADD CONSTRAINT customers_pkey PRIMARY KEY (customer_id);


        --
        -- Name: services services_pkey; Type: CONSTRAINT; Schema: public; Owner: freecodecamp
        --

        ALTER TABLE ONLY public.services
            ADD CONSTRAINT services_pkey PRIMARY KEY (service_id);


        --
        -- Name: appointments fk_customer_id; Type: FK CONSTRAINT; Schema: public; Owner: freecodecamp
        --

        ALTER TABLE ONLY public.appointments
            ADD CONSTRAINT fk_customer_id FOREIGN KEY (customer_id) REFERENCES public.customers(customer_id);


        --
        -- Name: appointments fk_service_id; Type: FK CONSTRAINT; Schema: public; Owner: freecodecamp
        --

        ALTER TABLE ONLY public.appointments
            ADD CONSTRAINT fk_service_id FOREIGN KEY (service_id) REFERENCES public.services(service_id);


        --
        -- PostgreSQL database dump complete
        --
        ```

## Attachment
- **Project workspace**: [Build a Salon Appointment Scheduler on freeCodeCamp](https://www.freecodecamp.org/learn/relational-database/build-a-salon-appointment-scheduler-project/build-a-salon-appointment-scheduler)
- **GitHub Repository**: [Salon Appointment Scheduler Repository](https://github.com/fahmiwazu/fcc-rdb-salondb)

