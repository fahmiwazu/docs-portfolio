# :material-database: Periodic Table Database

## Introduction
In the Build a Periodic Table Database project, I'll create a database to store information on chemical elements. I'll design tables, set up relationships, and run queries to explore element properties, strengthening my SQL skills while organizing scientific data.

## Role
- SQL Developer

## Goals

- **Design a Database Schema**: Create tables to store information about chemical elements, such as their names, symbols, atomic numbers, and properties.
- **Establish Relationships**: Set up relationships between tables, for example, linking elements to their respective groups or periods on the periodic table.
- **Perform CRUD Operations**: Implement SQL queries to create, read, update, and delete element data in the database.
- **Write Queries for Element Information**: Develop SQL queries to retrieve details about elements, such as their atomic mass, type, or placement on the periodic table.
- **Normalize the Database**: Ensure the database is normalized to avoid data redundancy and maintain data integrity.
- **Enhance SQL and Database Skills**: Improve skills in structuring, querying, and managing relational databases with scientific data.

## Resource Overview

??? abstract "Project Directory"
    === "Bash Atomic Libraty"
        ``` Bash title="element.sh"
        #!/bin/bash

        PSQL="psql --username=freecodecamp --dbname=periodic_table --no-align --tuples-only -c"
        
        
        #echo "Please provide an element as an argument."

        #echo $1
        if [[ $1 ]]
        then
        if [[ ! $1 =~ ^[0-9]+$ ]]
        then
            ELEMENT=$($PSQL "SELECT atomic_number, atomic_mass, melting_point_celsius, boiling_point_celsius, symbol,name, type FROM properties JOIN elements USING(atomic_number) JOIN types USING(type_id) WHERE elements.name LIKE '$1%' ORDER BY atomic_number LIMIT 1")
        else
            ELEMENT=$($PSQL "SELECT atomic_number, atomic_mass, melting_point_celsius, boiling_point_celsius, symbol,name, type FROM properties JOIN elements USING(atomic_number) JOIN types USING(type_id) WHERE elements.atomic_number=$1")
        fi
            if [[ -z $ELEMENT ]]
            then
            echo "I could not find that element in the database."
            else
            echo $ELEMENT | while IFS=\| read ATOMIC_NUMBER MASS MELT BOIL SYM NAME TYPE
            do
                echo "The element with atomic number $ATOMIC_NUMBER is $NAME ($SYM). It's a $TYPE, with a mass of $MASS amu. $NAME has a melting point of $MELT celsius and a boiling point of $BOIL celsius." 
            done
            fi
        else
        echo "Please provide an element as an argument."
        fi
        ```
    === "PosgreSQL Database Dump"
        ``` SQL title="periodic_table.sql"
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

        DROP DATABASE periodic_table;
        --
        -- Name: periodic_table; Type: DATABASE; Schema: -; Owner: postgres
        --

        CREATE DATABASE periodic_table WITH TEMPLATE = template0 ENCODING = 'UTF8' LC_COLLATE = 'C.UTF-8' LC_CTYPE = 'C.UTF-8';


        ALTER DATABASE periodic_table OWNER TO postgres;

        \connect periodic_table

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
        -- Name: elements; Type: TABLE; Schema: public; Owner: freecodecamp
        --

        CREATE TABLE public.elements (
            atomic_number integer NOT NULL,
            symbol character varying(2) NOT NULL,
            name character varying(40) NOT NULL
        );


        ALTER TABLE public.elements OWNER TO freecodecamp;

        --
        -- Name: properties; Type: TABLE; Schema: public; Owner: freecodecamp
        --

        CREATE TABLE public.properties (
            atomic_number integer NOT NULL,
            atomic_mass numeric NOT NULL,
            melting_point_celsius numeric NOT NULL,
            boiling_point_celsius numeric NOT NULL,
            type_id integer NOT NULL
        );


        ALTER TABLE public.properties OWNER TO freecodecamp;

        --
        -- Name: types; Type: TABLE; Schema: public; Owner: freecodecamp
        --

        CREATE TABLE public.types (
            type_id integer NOT NULL,
            type character varying(20) NOT NULL
        );


        ALTER TABLE public.types OWNER TO freecodecamp;

        --
        -- Data for Name: elements; Type: TABLE DATA; Schema: public; Owner: freecodecamp
        --

        INSERT INTO public.elements VALUES (1, 'H', 'Hydrogen');
        INSERT INTO public.elements VALUES (4, 'Be', 'Beryllium');
        INSERT INTO public.elements VALUES (5, 'B', 'Boron');
        INSERT INTO public.elements VALUES (6, 'C', 'Carbon');
        INSERT INTO public.elements VALUES (7, 'N', 'Nitrogen');
        INSERT INTO public.elements VALUES (8, 'O', 'Oxygen');
        INSERT INTO public.elements VALUES (2, 'He', 'Helium');
        INSERT INTO public.elements VALUES (3, 'Li', 'Lithium');
        INSERT INTO public.elements VALUES (9, 'F', 'Fluorine');
        INSERT INTO public.elements VALUES (10, 'Ne', 'Neon');


        --
        -- Data for Name: properties; Type: TABLE DATA; Schema: public; Owner: freecodecamp
        --

        INSERT INTO public.properties VALUES (2, 4, -272.2, -269, 1);
        INSERT INTO public.properties VALUES (6, 12, 3550, 4027, 1);
        INSERT INTO public.properties VALUES (7, 14, -210.1, -195.8, 1);
        INSERT INTO public.properties VALUES (8, 16, -218, -183, 1);
        INSERT INTO public.properties VALUES (3, 7, 180.54, 1342, 2);
        INSERT INTO public.properties VALUES (4, 9, 1287, 2470, 2);
        INSERT INTO public.properties VALUES (5, 11, 2075, 4000, 3);
        INSERT INTO public.properties VALUES (9, 18.998, -220, -188.1, 1);
        INSERT INTO public.properties VALUES (10, 20.18, -248.6, -246.1, 1);
        INSERT INTO public.properties VALUES (1, 1.008, -259.1, -252.9, 1);


        --
        -- Data for Name: types; Type: TABLE DATA; Schema: public; Owner: freecodecamp
        --

        INSERT INTO public.types VALUES (1, 'nonmetal');
        INSERT INTO public.types VALUES (2, 'metal');
        INSERT INTO public.types VALUES (3, 'metalloid');


        --
        -- Name: elements elements_atomic_number_key; Type: CONSTRAINT; Schema: public; Owner: freecodecamp
        --

        ALTER TABLE ONLY public.elements
            ADD CONSTRAINT elements_atomic_number_key UNIQUE (atomic_number);


        --
        -- Name: elements elements_name_key; Type: CONSTRAINT; Schema: public; Owner: freecodecamp
        --

        ALTER TABLE ONLY public.elements
            ADD CONSTRAINT elements_name_key UNIQUE (name);


        --
        -- Name: elements elements_pkey; Type: CONSTRAINT; Schema: public; Owner: freecodecamp
        --

        ALTER TABLE ONLY public.elements
            ADD CONSTRAINT elements_pkey PRIMARY KEY (atomic_number);


        --
        -- Name: elements elements_symbol_key; Type: CONSTRAINT; Schema: public; Owner: freecodecamp
        --

        ALTER TABLE ONLY public.elements
            ADD CONSTRAINT elements_symbol_key UNIQUE (symbol);


        --
        -- Name: properties properties_atomic_number_key; Type: CONSTRAINT; Schema: public; Owner: freecodecamp
        --

        ALTER TABLE ONLY public.properties
            ADD CONSTRAINT properties_atomic_number_key UNIQUE (atomic_number);


        --
        -- Name: properties properties_pkey; Type: CONSTRAINT; Schema: public; Owner: freecodecamp
        --

        ALTER TABLE ONLY public.properties
            ADD CONSTRAINT properties_pkey PRIMARY KEY (atomic_number);


        --
        -- Name: types types_pkey; Type: CONSTRAINT; Schema: public; Owner: freecodecamp
        --

        ALTER TABLE ONLY public.types
            ADD CONSTRAINT types_pkey PRIMARY KEY (type_id);


        --
        -- Name: properties fk_atomic_number; Type: FK CONSTRAINT; Schema: public; Owner: freecodecamp
        --

        ALTER TABLE ONLY public.properties
            ADD CONSTRAINT fk_atomic_number FOREIGN KEY (atomic_number) REFERENCES public.elements(atomic_number);


        --
        -- Name: properties properties_type_id_fkey; Type: FK CONSTRAINT; Schema: public; Owner: freecodecamp
        --

        ALTER TABLE ONLY public.properties
            ADD CONSTRAINT properties_type_id_fkey FOREIGN KEY (type_id) REFERENCES public.types(type_id);


        --
        -- PostgreSQL database dump complete
        --
        ```

## Attachment
- **Project workspace**: [Build a Periodic Table Database on freeCodeCamp](https://www.freecodecamp.org/learn/relational-database/build-a-periodic-table-database-project/build-a-periodic-table-database)
- **GitHub Repository**: [Periodic Table Repository](https://github.com/fahmiwazu/fcc-rdb-atomicdb)
