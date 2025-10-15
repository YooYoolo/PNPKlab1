# Лабораторная работа №1: UML Диаграммы классов  
## Система IT-поддержки (Вариант №8)

---

## UML Диаграмма классов

```plantuml
@startuml
title "UML Диаграмма классов - Система IT-поддержки"

skinparam classAttributeIconSize 0
skinparam arrowThickness 1
skinparam classFontSize 14
skinparam shadowing false
skinparam linetype ortho

interface IUser {
    + getName(): string
}

class Employee {
    - id: int
    - name: string
    + getName(): string
    + createTicket(description: string, ticketId: int): Ticket
}

class Technician {
    - id: int
    - name: string
    - assignedTickets: vector<Ticket*>
    + getName(): string
    + assignTicket(ticket: Ticket): void
    + changeStatus(ticket: Ticket, status: Status): void
}

class SeniorTechnician {
    + escalate(ticket: Ticket): void
}

class Ticket {
    - id: int
    - description: string
    - status: Status
    - creator: Employee*
    - assignedTo: Technician*
    + getId(): int
    + getDescription(): string
    + getStatus(): Status
    + setStatus(s: Status): void
}

class KnowledgeBase {
    - tickets: vector<Ticket*>
    + addTicket(ticket: Ticket): void
    + listTickets(): void
    + getStats(): void
}

enum Status {
    OPEN
    IN_PROGRESS
    RESOLVED
    CLOSED
}

Employee ..|> IUser
Technician ..|> IUser
SeniorTechnician --|> Technician

Employee --> "0..*" Ticket
Technician --> "0..*" Ticket
KnowledgeBase o-- "0..*" Ticket

@enduml

