Certainly! Here is the updated **README** file with instructions to use `python app.py` instead of `flask run`:

---

# Superhero API

This project is a **Flask RESTful API** designed to manage superheroes and their powers. The API allows you to create, read, update, and delete superheroes, powers, and the relationships between them.

## Table of Contents
- [Installation](#installation)
- [Usage](#usage)
- [API Endpoints](#api-endpoints)
- [Models](#models)
- [Validations](#validations)
- [Migrations](#migrations)
- [Seeding the Database](#seeding-the-database)
- [Testing](#testing)
- [Contributing](#contributing)
- [License](#license)

## Installation

### Requirements
To run this project, you need the following installed on your machine:
- Python 3.x
- Flask
- Flask-SQLAlchemy
- Flask-Migrate
- SQLite (default, but can be configured for other databases)

### Setup

1. **Clone the repository:**
   ```bash
  git remote add origin git@github.com:Snappyhacker/superheroes2.git
  git
   cd superhero-api
   ```

2. **Create and activate a virtual environment:**
   ```bash
   python3 -m venv venv
   source venv/bin/activate  # On Windows use: venv\Scripts\activate
   ```

3. **Install the required dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

4. **Run database migrations:**
   ```bash
   python app.py db upgrade
   ```

5. **Seed the database (optional but useful for testing):**
   ```bash
   python seed.py
   ```

6. **Start the Flask development server:**
   ```bash
   python3 app.py
   ```

7. **Access the API:**
   The server will run on `http://127.0.0.1:5000/`. You can interact with it using Postman, `curl`, or a browser.

---

## Usage

You can use tools like **Postman** or `curl` to interact with the API.

To make a **GET** request to the `/heroes` endpoint using `curl`, for example:
```bash
curl http://127.0.0.1:5000/heroes
```

In Postman:
1. Open Postman.
2. Create a new request.
3. Choose `GET` and enter `http://127.0.0.1:5000/heroes`.
4. Press **Send** to view the response.

---

## API Endpoints

Here’s a list of available API endpoints, their methods, and example requests/responses:

### **Heroes**

- **GET** `/heroes`
  - **Description**: Retrieve all heroes.
  - **Response**:
    ```json
    [
      {
        "id": 1,
        "name": "Kamala Khan",
        "super_name": "Ms. Marvel"
      }
    ]
    ```

- **GET** `/heroes/<id>`
  - **Description**: Retrieve a specific hero by ID.
  - **Response**:
    ```json
    {
      "id": 1,
      "name": "Kamala Khan",
      "super_name": "Ms. Marvel",
      "hero_powers": [
        {
          "id": 1,
          "strength": "Strong",
          "power": {
            "id": 2,
            "name": "Flight",
            "description": "Gives the ability to fly at supersonic speeds."
          }
        }
      ]
    }
    ```

### **Powers**

- **GET** `/powers`
  - **Description**: Retrieve all powers.
  - **Response**:
    ```json
    [
      {
        "id": 1,
        "name": "Super Strength",
        "description": "Gives the wielder super-human strength."
      }
    ]
    ```

- **GET** `/powers/<id>`
  - **Description**: Retrieve a specific power by ID.
  - **Response**:
    ```json
    {
      "id": 1,
      "name": "Super Strength",
      "description": "Gives the wielder super-human strength."
    }
    ```

- **PATCH** `/powers/<id>`
  - **Description**: Update a power's description.
  - **Request**:
    ```json
    {
      "description": "Updated description for super strength."
    }
    ```
  - **Response**:
    ```json
    {
      "id": 1,
      "name": "Super Strength",
      "description": "Updated description for super strength."
    }
    ```

### **Hero Powers**

- **POST** `/hero_powers`
  - **Description**: Create a new `HeroPower` relationship between a hero and a power.
  - **Request**:
    ```json
    {
      "strength": "Average",
      "hero_id": 1,
      "power_id": 2
    }
    ```
  - **Response**:
    ```json
    {
      "id": 10,
      "hero_id": 1,
      "power_id": 2,
      "strength": "Average",
      "hero": {
        "id": 1,
        "name": "Kamala Khan",
        "super_name": "Ms. Marvel"
      },
      "power": {
        "id": 2,
        "name": "Flight",
        "description": "Gives the ability to fly at supersonic speeds."
      }
    }
    ```

---

## Models

- **Hero**:
  - Attributes:
    - `id`: Integer, Primary Key.
    - `name`: String, the real name of the hero.
    - `super_name`: String, the superhero name.
  - Relationships: Has many `HeroPower`s.

- **Power**:
  - Attributes:
    - `id`: Integer, Primary Key.
    - `name`: String, the name of the power.
    - `description`: String, at least 20 characters long.
  - Relationships: Has many `HeroPower`s.

- **HeroPower**:
  - Attributes:
    - `id`: Integer, Primary Key.
    - `strength`: String, one of 'Strong', 'Weak', or 'Average'.
  - Relationships: Belongs to a `Hero` and a `Power`.

---

## Validations

The following validations are enforced in the models:

- **HeroPower**:
  - `strength` must be one of the following values: `'Strong', 'Weak', 'Average'`.

- **Power**:
  - `description` must be present and at least 20 characters long.

---

## Migrations

Database migrations are handled using Flask-Migrate. To run migrations:

1. **Initialize migrations**:
   ```bash
   python app.py db init
   ```

2. **Create a migration** (after making changes to models):
   ```bash
   python app.py db migrate -m "Initial migration"
   ```

3. **Apply migrations**:
   ```bash
   python app.py db upgrade
   ```

---

## Seeding the Database

To populate the database with initial data, run the following command:

```bash
python seed.py
```

This will add sample heroes and powers to the database, which can then be retrieved through the API.

---

## Testing

You can test the API using tools like **Postman** or `curl` by sending requests to the various endpoints listed above.

### Example using `curl`:
```bash
curl http://127.0.0.1:5000/heroes
```

### Example using Postman:
1. Create a new request.
2. Enter `GET http://127.0.0.1:5000/heroes`.
3. Click **Send** to view the response.

---

## Contributing

Contributions are welcome! To contribute:

1. Fork this repository.
2. Create a feature branch (`git checkout -b feature-branch`).
3. Commit your changes (`git commit -m 'Add feature'`).
4. Push to the branch (`git push origin feature-branch`).
5. Open a pull request.

---

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

---

### Final Note:

- Make sure to review and test all API endpoints before submitting.
- Ensure that your database is properly migrated and seeded for testing.
- Validate the response structures using Postman or `curl`.

---
