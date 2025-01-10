# :material-database: Celestial Bodies Database

## Introduction
In the Celestial Bodies project, I'll create a database to store data about planets, moons, stars, and galaxies. I'll design tables, set up relationships, and run queries, building my SQL and database skills while organizing astronomical data.

## Role
- SQL Developer

## Goals

- **Design a Database Schema**: Create tables to store information about celestial bodies, including planets, moons, stars, and galaxies.
- **Establish Relationships**: Set up relationships between tables, such as linking moons to their respective planets.
- **Perform CRUD Operations**: Implement and practice basic SQL operations (Create, Read, Update, Delete) to manage celestial body data.
- **Write Complex Queries**: Write SQL queries to retrieve specific information, such as finding planets with the most moons or galaxies within a certain distance.
- **Normalize the Database**: Organize data efficiently by ensuring the database is normalized to reduce redundancy and improve data integrity.
- **Enhance SQL Skills**: Strengthen our ability to design and query relational databases through practical, hands-on experience.

## Resource Overview

??? abstract "PostgreSQL Database Dump"
    ``` SQL title="universe.sql"
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
    
    DROP DATABASE universe;
    --
    -- Name: universe; Type: DATABASE; Schema: -; Owner: freecodecamp
    --
    
    CREATE DATABASE universe WITH TEMPLATE = template0 ENCODING = 'UTF8' LC_COLLATE = 'C.UTF-8' LC_CTYPE = 'C.UTF-8';
    
    
    ALTER DATABASE universe OWNER TO freecodecamp;
    
    \connect universe
    
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
    -- Name: blackhole; Type: TABLE; Schema: public; Owner: freecodecamp
    --
    
    CREATE TABLE public.blackhole (
        blackhole_id integer NOT NULL,
        gravity integer,
        galaxy_id integer,
        wormhole boolean DEFAULT false NOT NULL,
        speed integer NOT NULL,
        name character varying(255)
    );
    
    
    ALTER TABLE public.blackhole OWNER TO freecodecamp;
    
    --
    -- Name: blackhole_blackhole_id_seq; Type: SEQUENCE; Schema: public; Owner: freecodecamp
    --
    
    CREATE SEQUENCE public.blackhole_blackhole_id_seq
        AS integer
        START WITH 1
        INCREMENT BY 1
        NO MINVALUE
        NO MAXVALUE
        CACHE 1;
    
    
    ALTER TABLE public.blackhole_blackhole_id_seq OWNER TO freecodecamp;
    
    --
    -- Name: blackhole_blackhole_id_seq; Type: SEQUENCE OWNED BY; Schema: public; Owner: freecodecamp
    --
    
    ALTER SEQUENCE public.blackhole_blackhole_id_seq OWNED BY public.blackhole.blackhole_id;
    
    
    --
    -- Name: galaxy; Type: TABLE; Schema: public; Owner: freecodecamp
    --
    
    CREATE TABLE public.galaxy (
        galaxy_id integer NOT NULL,
        speed integer,
        description text,
        name character varying(255) NOT NULL,
        rotation_speed integer DEFAULT 100000000 NOT NULL,
        total_mass integer
    );
    
    
    ALTER TABLE public.galaxy OWNER TO freecodecamp;
    
    --
    -- Name: galaxy_galaxy_id_seq; Type: SEQUENCE; Schema: public; Owner: freecodecamp
    --
    
    CREATE SEQUENCE public.galaxy_galaxy_id_seq
        AS integer
        START WITH 1
        INCREMENT BY 1
        NO MINVALUE
        NO MAXVALUE
        CACHE 1;
    
    
    ALTER TABLE public.galaxy_galaxy_id_seq OWNER TO freecodecamp;
    
    --
    -- Name: galaxy_galaxy_id_seq; Type: SEQUENCE OWNED BY; Schema: public; Owner: freecodecamp
    --
    
    ALTER SEQUENCE public.galaxy_galaxy_id_seq OWNED BY public.galaxy.galaxy_id;
    
    
    --
    -- Name: moon; Type: TABLE; Schema: public; Owner: freecodecamp
    --
    
    CREATE TABLE public.moon (
        moon_id integer NOT NULL,
        name character varying(255) NOT NULL,
        has_water boolean NOT NULL,
        planet_id integer NOT NULL,
        name_code character varying(255) NOT NULL
    );
    
    
    ALTER TABLE public.moon OWNER TO freecodecamp;
    
    --
    -- Name: moon_moon_id_seq; Type: SEQUENCE; Schema: public; Owner: freecodecamp
    --
    
    CREATE SEQUENCE public.moon_moon_id_seq
        AS integer
        START WITH 1
        INCREMENT BY 1
        NO MINVALUE
        NO MAXVALUE
        CACHE 1;
    
    
    ALTER TABLE public.moon_moon_id_seq OWNER TO freecodecamp;
    
    --
    -- Name: moon_moon_id_seq; Type: SEQUENCE OWNED BY; Schema: public; Owner: freecodecamp
    --
    
    ALTER SEQUENCE public.moon_moon_id_seq OWNED BY public.moon.moon_id;
    
    
    --
    -- Name: planet; Type: TABLE; Schema: public; Owner: freecodecamp
    --
    
    CREATE TABLE public.planet (
        planet_id integer NOT NULL,
        name character varying(255) NOT NULL,
        time_travel boolean DEFAULT false NOT NULL,
        star_id integer NOT NULL,
        people numeric
    );
    
    
    ALTER TABLE public.planet OWNER TO freecodecamp;
    
    --
    -- Name: planet_planet_id_seq; Type: SEQUENCE; Schema: public; Owner: freecodecamp
    --
    
    CREATE SEQUENCE public.planet_planet_id_seq
        AS integer
        START WITH 1
        INCREMENT BY 1
        NO MINVALUE
        NO MAXVALUE
        CACHE 1;
    
    
    ALTER TABLE public.planet_planet_id_seq OWNER TO freecodecamp;
    
    --
    -- Name: planet_planet_id_seq; Type: SEQUENCE OWNED BY; Schema: public; Owner: freecodecamp
    --
    
    ALTER SEQUENCE public.planet_planet_id_seq OWNED BY public.planet.planet_id;
    
    
    --
    -- Name: star; Type: TABLE; Schema: public; Owner: freecodecamp
    --
    
    CREATE TABLE public.star (
        star_id integer NOT NULL,
        radius integer NOT NULL,
        color character varying(255) NOT NULL,
        name character varying(255) NOT NULL,
        galaxy_id integer,
        mass integer
    );
    
    
    ALTER TABLE public.star OWNER TO freecodecamp;
    
    --
    -- Name: star_star_id_seq; Type: SEQUENCE; Schema: public; Owner: freecodecamp
    --
    
    CREATE SEQUENCE public.star_star_id_seq
        AS integer
        START WITH 1
        INCREMENT BY 1
        NO MINVALUE
        NO MAXVALUE
        CACHE 1;
    
    
    ALTER TABLE public.star_star_id_seq OWNER TO freecodecamp;
    
    --
    -- Name: star_star_id_seq; Type: SEQUENCE OWNED BY; Schema: public; Owner: freecodecamp
    --
    
    ALTER SEQUENCE public.star_star_id_seq OWNED BY public.star.star_id;
    
    
    --
    -- Name: blackhole blackhole_id; Type: DEFAULT; Schema: public; Owner: freecodecamp
    --
    
    ALTER TABLE ONLY public.blackhole ALTER COLUMN blackhole_id SET DEFAULT nextval('public.blackhole_blackhole_id_seq'::regclass);
    
    
    --
    -- Name: galaxy galaxy_id; Type: DEFAULT; Schema: public; Owner: freecodecamp
    --
    
    ALTER TABLE ONLY public.galaxy ALTER COLUMN galaxy_id SET DEFAULT nextval('public.galaxy_galaxy_id_seq'::regclass);
    
    
    --
    -- Name: moon moon_id; Type: DEFAULT; Schema: public; Owner: freecodecamp
    --
    
    ALTER TABLE ONLY public.moon ALTER COLUMN moon_id SET DEFAULT nextval('public.moon_moon_id_seq'::regclass);
    
    
    --
    -- Name: planet planet_id; Type: DEFAULT; Schema: public; Owner: freecodecamp
    --
    
    ALTER TABLE ONLY public.planet ALTER COLUMN planet_id SET DEFAULT nextval('public.planet_planet_id_seq'::regclass);
    
    
    --
    -- Name: star star_id; Type: DEFAULT; Schema: public; Owner: freecodecamp
    --
    
    ALTER TABLE ONLY public.star ALTER COLUMN star_id SET DEFAULT nextval('public.star_star_id_seq'::regclass);
    
    
    --
    -- Data for Name: blackhole; Type: TABLE DATA; Schema: public; Owner: freecodecamp
    --
    
    INSERT INTO public.blackhole VALUES (1, NULL, NULL, false, 10000000, NULL);
    INSERT INTO public.blackhole VALUES (2, NULL, NULL, false, 10000010, NULL);
    INSERT INTO public.blackhole VALUES (3, NULL, NULL, false, 10000020, NULL);
    INSERT INTO public.blackhole VALUES (4, NULL, NULL, false, 10000320, NULL);
    INSERT INTO public.blackhole VALUES (5, NULL, NULL, false, 10000340, NULL);
    
    
    --
    -- Data for Name: galaxy; Type: TABLE DATA; Schema: public; Owner: freecodecamp
    --
    
    INSERT INTO public.galaxy VALUES (1, NULL, NULL, 'bimasakti', 100000000, NULL);
    INSERT INTO public.galaxy VALUES (2, NULL, NULL, 'galaxy2', 100000000, NULL);
    INSERT INTO public.galaxy VALUES (3, NULL, NULL, 'galaxy3', 100000000, NULL);
    INSERT INTO public.galaxy VALUES (4, NULL, NULL, 'galaxy4', 100000000, NULL);
    INSERT INTO public.galaxy VALUES (5, NULL, NULL, 'galaxy5', 100000000, NULL);
    INSERT INTO public.galaxy VALUES (6, NULL, NULL, 'galaxy6', 100000000, NULL);
    
    
    --
    -- Data for Name: moon; Type: TABLE DATA; Schema: public; Owner: freecodecamp
    --
    
    INSERT INTO public.moon VALUES (1, 'moon1', true, 1, 'moon1');
    INSERT INTO public.moon VALUES (2, 'moon2', true, 2, 'moon2');
    INSERT INTO public.moon VALUES (3, 'moon3', true, 3, 'moon3');
    INSERT INTO public.moon VALUES (4, 'moon4', true, 4, 'moon4');
    INSERT INTO public.moon VALUES (5, 'moon5', true, 5, 'moon5');
    INSERT INTO public.moon VALUES (6, 'moon5', true, 5, 'moon6');
    INSERT INTO public.moon VALUES (7, 'moon5', true, 5, 'moon7');
    INSERT INTO public.moon VALUES (8, 'moon5', true, 5, 'moon8');
    INSERT INTO public.moon VALUES (9, 'moon5', true, 5, 'moon9');
    INSERT INTO public.moon VALUES (10, 'moon5', true, 5, 'moon10');
    INSERT INTO public.moon VALUES (11, 'moon5', true, 5, 'moon11');
    INSERT INTO public.moon VALUES (12, 'moon5', true, 5, 'moon12');
    INSERT INTO public.moon VALUES (13, 'moon5', true, 5, 'moon13');
    INSERT INTO public.moon VALUES (14, 'moon5', true, 5, 'moon14');
    INSERT INTO public.moon VALUES (15, 'moon5', true, 5, 'moon15');
    INSERT INTO public.moon VALUES (16, 'moon5', true, 5, 'moon16');
    INSERT INTO public.moon VALUES (17, 'moon5', true, 5, 'moon17');
    INSERT INTO public.moon VALUES (18, 'moon5', true, 5, 'moon18');
    INSERT INTO public.moon VALUES (19, 'moon5', true, 5, 'moon19');
    INSERT INTO public.moon VALUES (20, 'moon5', true, 5, 'moon20');
    INSERT INTO public.moon VALUES (21, 'moon5', true, 5, 'moon21');
    
    
    --
    -- Data for Name: planet; Type: TABLE DATA; Schema: public; Owner: freecodecamp
    --
    
    INSERT INTO public.planet VALUES (1, 'earth', false, 1, NULL);
    INSERT INTO public.planet VALUES (2, 'mars', false, 1, NULL);
    INSERT INTO public.planet VALUES (3, 'venus', false, 1, NULL);
    INSERT INTO public.planet VALUES (4, 'saturnus', false, 1, NULL);
    INSERT INTO public.planet VALUES (5, 'jupiter', false, 1, NULL);
    INSERT INTO public.planet VALUES (6, 'uranus', false, 1, NULL);
    INSERT INTO public.planet VALUES (7, 'mercury', false, 1, NULL);
    INSERT INTO public.planet VALUES (8, 'hello', false, 2, NULL);
    INSERT INTO public.planet VALUES (9, 'bro', false, 2, NULL);
    INSERT INTO public.planet VALUES (10, 'waz', false, 3, NULL);
    INSERT INTO public.planet VALUES (11, 'cal', false, 3, NULL);
    INSERT INTO public.planet VALUES (12, 'uhuy', false, 3, NULL);
    INSERT INTO public.planet VALUES (13, 'mamang', false, 3, NULL);
    
    
    --
    -- Data for Name: star; Type: TABLE DATA; Schema: public; Owner: freecodecamp
    --
    
    INSERT INTO public.star VALUES (1, 123124123, 'red', 'matahari', 1, NULL);
    INSERT INTO public.star VALUES (2, 123124123, 'red', 'spongebob', 1, NULL);
    INSERT INTO public.star VALUES (3, 123124123, 'red', 'pactrick', 1, NULL);
    INSERT INTO public.star VALUES (4, 123124123, 'red', 'sandy', 2, NULL);
    INSERT INTO public.star VALUES (5, 123124123, 'red', 'mr.krab', 3, NULL);
    INSERT INTO public.star VALUES (6, 123124123, 'red', 'squidward', 3, NULL);
    
    
    --
    -- Name: blackhole_blackhole_id_seq; Type: SEQUENCE SET; Schema: public; Owner: freecodecamp
    --
    
    SELECT pg_catalog.setval('public.blackhole_blackhole_id_seq', 5, true);
    
    
    --
    -- Name: galaxy_galaxy_id_seq; Type: SEQUENCE SET; Schema: public; Owner: freecodecamp
    --
    
    SELECT pg_catalog.setval('public.galaxy_galaxy_id_seq', 6, true);
    
    
    --
    -- Name: moon_moon_id_seq; Type: SEQUENCE SET; Schema: public; Owner: freecodecamp
    --
    
    SELECT pg_catalog.setval('public.moon_moon_id_seq', 21, true);
    
    
    --
    -- Name: planet_planet_id_seq; Type: SEQUENCE SET; Schema: public; Owner: freecodecamp
    --
    
    SELECT pg_catalog.setval('public.planet_planet_id_seq', 13, true);
    
    
    --
    -- Name: star_star_id_seq; Type: SEQUENCE SET; Schema: public; Owner: freecodecamp
    --
    
    SELECT pg_catalog.setval('public.star_star_id_seq', 6, true);
    
    
    --
    -- Name: blackhole blackhole_pkey; Type: CONSTRAINT; Schema: public; Owner: freecodecamp
    --
    
    ALTER TABLE ONLY public.blackhole
        ADD CONSTRAINT blackhole_pkey PRIMARY KEY (blackhole_id);
    
    
    --
    -- Name: blackhole blackhole_speed_key; Type: CONSTRAINT; Schema: public; Owner: freecodecamp
    --
    
    ALTER TABLE ONLY public.blackhole
        ADD CONSTRAINT blackhole_speed_key UNIQUE (speed);
    
    
    --
    -- Name: galaxy galaxy_pkey; Type: CONSTRAINT; Schema: public; Owner: freecodecamp
    --
    
    ALTER TABLE ONLY public.galaxy
        ADD CONSTRAINT galaxy_pkey PRIMARY KEY (galaxy_id);
    
    
    --
    -- Name: galaxy galaxy_total_mass_key; Type: CONSTRAINT; Schema: public; Owner: freecodecamp
    --
    
    ALTER TABLE ONLY public.galaxy
        ADD CONSTRAINT galaxy_total_mass_key UNIQUE (total_mass);
    
    
    --
    -- Name: moon moon_name_code_key; Type: CONSTRAINT; Schema: public; Owner: freecodecamp
    --
    
    ALTER TABLE ONLY public.moon
        ADD CONSTRAINT moon_name_code_key UNIQUE (name_code);
    
    
    --
    -- Name: moon moon_pkey; Type: CONSTRAINT; Schema: public; Owner: freecodecamp
    --
    
    ALTER TABLE ONLY public.moon
        ADD CONSTRAINT moon_pkey PRIMARY KEY (moon_id);
    
    
    --
    -- Name: planet planet_people_key; Type: CONSTRAINT; Schema: public; Owner: freecodecamp
    --
    
    ALTER TABLE ONLY public.planet
        ADD CONSTRAINT planet_people_key UNIQUE (people);
    
    
    --
    -- Name: planet planet_pkey; Type: CONSTRAINT; Schema: public; Owner: freecodecamp
    --
    
    ALTER TABLE ONLY public.planet
        ADD CONSTRAINT planet_pkey PRIMARY KEY (planet_id);
    
    
    --
    -- Name: star star_mass_key; Type: CONSTRAINT; Schema: public; Owner: freecodecamp
    --
    
    ALTER TABLE ONLY public.star
        ADD CONSTRAINT star_mass_key UNIQUE (mass);
    
    
    --
    -- Name: star star_pkey; Type: CONSTRAINT; Schema: public; Owner: freecodecamp
    --
    
    ALTER TABLE ONLY public.star
        ADD CONSTRAINT star_pkey PRIMARY KEY (star_id);
    
    
    --
    -- Name: star fk_galaxy; Type: FK CONSTRAINT; Schema: public; Owner: freecodecamp
    --
    
    ALTER TABLE ONLY public.star
        ADD CONSTRAINT fk_galaxy FOREIGN KEY (galaxy_id) REFERENCES public.galaxy(galaxy_id);
    
    
    --
    -- Name: moon fk_planet; Type: FK CONSTRAINT; Schema: public; Owner: freecodecamp
    --
    
    ALTER TABLE ONLY public.moon
        ADD CONSTRAINT fk_planet FOREIGN KEY (planet_id) REFERENCES public.planet(planet_id);
    
    
    --
    -- Name: planet fk_star; Type: FK CONSTRAINT; Schema: public; Owner: freecodecamp
    --
    
    ALTER TABLE ONLY public.planet
        ADD CONSTRAINT fk_star FOREIGN KEY (star_id) REFERENCES public.star(star_id);
    
    
    --
    -- PostgreSQL database dump complete
    --
    ```

## Attachment

- **Project workspace**: [Build a Celestial Bodies Database on freeCodeCamp](https://www.freecodecamp.org/learn/relational-database/build-a-celestial-bodies-database-project/build-a-celestial-bodies-database)
- **GitHub Repository**: [Celestial Bodies Repository](https://github.com/fahmiwazu/fcc-rdb-celestialdb)