# Webdriver Database

Relational database project developed by **Group 4** for the
**INF1930 — Database Project** course at
**Universidade Católica de Pernambuco (UNICAP)**.

The project models and implements the database of **Webdriver**, a file
management platform that supports users, files, sharing, institutions,
plans, support requests, operations, and file version history.

---

## About the Project

The goal of this project is to apply relational database design concepts
through the development of a complete database solution.

The project covers:

- Conceptual data modeling
- Logical data modeling
- Physical database modeling
- SQL
- CRUD operations
- Integrity constraints
- Access control
- Views
- Roles and permissions
- Stored procedures
- Functions
- Triggers
- Database testing

The implementation must use **SQL and a supporting programming language**.

---

## Domain

Webdriver is a file storage and management platform.

The database represents entities and relationships involving:

- Users
- Files
- File ownership
- File sharing
- File operations
- Comments
- Institutions
- Plans
- Administrators
- Support requests
- File version history

Users can own and share files with other users.

Operations performed on files must be registered with their respective
date and time, and files maintain a version history containing information
about modifications.

Institutions can contain multiple users and subscribe to a plan.

Administrators provide support to users, including requests associated
with specific files.

---

# Project Scope

The project is divided into two main stages.

## Part 1 — Database Foundation

The first stage establishes the core database structure and operations.

### Data Modeling

- Conceptual model
- Logical model
- Physical model

### Core Operations

The physical implementation must support:

- Database creation
- Insert
- Search
- Update
- Delete

### Main Domain Requirements

The database must represent:

- Users and their files
- File metadata
- File ownership
- File sharing
- File operations
- Comments
- Institutions
- Plans
- Administrators
- Support relationships
- Support requests
- File version history

---

## Part 2 — Advanced Database Features

The second stage extends the database with access control,
procedural SQL, and automation.

### Recent Activities

A new table called:

`Atividades_recentes`

must be created to track file activity.

It contains:

- File reference
- Date of the latest modification
- Access priority

Access priority can be:

- Priority
- Non-priority

Only the **Root** user should have direct access to this table.

---

## Views

The project must provide views that ensure users only see
information they are allowed to access.

Required behavior includes:

- Users only see files they own or have permission to access
- Institutions can view their users and related files
- Administrators can access the database according to their permissions
- Users can view operation history without modifying it
- Internal IDs must be hidden from user-facing views

---

## Roles and Permissions

Three main database roles must be implemented.

### `PapelUsuario`

Can:

- Select accessible files
- Insert files
- Update files for which the user has permission

### `PapelEmpresa`

Can view:

- Users belonging to the institution
- Files belonging to institution users

This role should have read-only access to these resources.

### `PapelAdm`

Can:

- Select
- Insert
- Update
- Delete

across the database, subject to the explicit restrictions defined
for protected resources.

---

## Stored Procedures

The following procedures must be implemented.

### `Verificar_atividades`

Updates the `Atividades_recentes` table according to the project requirement.

### `Conta_usuarios`

Receives a file identifier and returns the number of distinct users
with access to that file.

### `Chavear`

Toggles a file between:

- Priority
- Non-priority

### `Remover_acessos`

Receives a file identifier and removes shared access while preserving
the file owner's access.

---

## Functions

A function must determine whether more than **100 days** have passed
since the last modification of a file.

Expected result:

- `TRUE` — more than 100 days
- `FALSE` — 100 days or fewer

---

## Triggers

### `Safe_security`

Prevents executable files from being inserted into the drive.

### `Registrar_operacao`

Whenever a new file operation is registered, the corresponding
recent activity information must be updated.

### `Atualizar_acesso`

Whenever a user receives access to a new file, the related file
records must also be updated.

---

# Repository Structure

The repository is expected to evolve toward the following organization:
