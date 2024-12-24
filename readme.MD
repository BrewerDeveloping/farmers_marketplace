# Farmers Marketplace Project Setup

This guide provides detailed instructions for setting up the Farmers Marketplace project on any device.

---

## Prerequisites
Before starting, ensure the following tools are installed on your device:

- **Ruby** (version 3.2.2)
- **Rails** (version 8.0.1)
- **PostgreSQL**
- **Node.js**
- **Yarn**
- **Git**

### Recommended Tools
- **Docker** (optional, for containerized development)
- **Text Editor/IDE**: VS Code or another editor of your choice.

---

## Step 1: Clone the Repository
Clone the project repository from GitHub:

```bash
# Replace <username> with your GitHub username
git clone https://github.com/brewerdeveloping/farmers_marketplace.git
cd farmers_marketplace
```

---

## Step 2: Install Ruby and Rails Dependencies

### Install Ruby
If Ruby is not already installed, use a version manager like `rbenv`:

```bash
rbenv install 3.2.2
rbenv global 3.2.2
```

Verify the installation:
```bash
ruby -v
```

### Install Rails
Install Rails globally:

```bash
gem install rails
```

Verify the installation:
```bash
rails -v
```

---

## Step 3: Install Project Dependencies

### Install Gems
Run `bundle install` to install all required gems from the `requirements.txt` file:

```bash
bundle install
```

### Install Frontend Dependencies
Use Yarn to install frontend packages:

```bash
yarn install
```

---

## Step 4: Set Up the Database

### Configure PostgreSQL
1. Update `config/database.yml` with your PostgreSQL username and password.
2. Create the database:

```bash
rails db:create
```

3. Run migrations:

```bash
rails db:migrate
```

---

## Step 5: Start the Development Server

Run the Rails server locally:

```bash
rails server
```

Visit `http://localhost:3000` to see the application.

---

## Optional: Dockerized Environment

### Build the Docker Image
Create a `Dockerfile` and `docker-compose.yml` for containerized development.

#### Dockerfile:
```dockerfile
FROM ruby:3.2.2
WORKDIR /app
COPY Gemfile Gemfile.lock /app/
RUN bundle install
COPY . /app
CMD ["rails", "server", "-b", "0.0.0.0"]
```

#### docker-compose.yml:
```yaml
version: "3.9"
services:
  app:
    build: .
    ports:
      - "3000:3000"
    volumes:
      - ".:/app"
    depends_on:
      - db
  db:
    image: postgres
    environment:
      POSTGRES_USER: user
      POSTGRES_PASSWORD: password
      POSTGRES_DB: farmers_marketplace
    ports:
      - "5432:5432"
```

### Start Docker Containers
Run the containers:

```bash
docker-compose up --build
```

---

## Testing and Deployment

### Run Tests
Run all test cases:

```bash
rspec
```

### Deploy to Production
Use a platform like Render, Heroku, or AWS Free Tier. Example for Heroku:

```bash
heroku login
heroku create
heroku buildpacks:set heroku/ruby
heroku buildpacks:add --index 1 heroku/nodejs
git push heroku main
```

---

## Additional Notes
- Refer to `requirements.txt` for all project dependencies.
- Use `.env` files (managed by `dotenv-rails`) to store sensitive information like database credentials.


# Breakdown of Included Technologies

- **Ruby Version**: Matches the version used in development (3.2.2).
- **Rails Framework**: Includes Rails 8.0.1 for the core application.
- **PostgreSQL (pg gem)**: Covers the database requirement.
- **Webpacker & Yarn**: Prepares for front-end integration with a framework like React (future step).
- **Authentication & Authorization**: bcrypt for user authentication and pundit for simple policy management.
- **Pagination**: kaminari is included to paginate marketplace listings.
- **Notifications**: sidekiq (for background jobs) and actioncable (real-time updates).
- **Testing**: Comprehensive tools (rspec, capybara, factory_bot) for TDD/BDD.
- **DevOps**: puma for web server configuration and foreman for managing development processes.

# Usage Instructions

1. Save the file as `requirements.txt` in your project’s root directory.
2. When setting up on a new device:
    - Ensure bundler is installed:
      ```sh
      gem install bundler
      ```
    - Install all gems:
      ```sh
      bundle install
      ```

