 cargo new --lib diesel_demo
cargo install diesel_cli
cargo install diesel_cli --no-default-features --features postgres
echo DATABASE_URL=postgres://username:password@localhost/diesel_demo > .env
diesel migration generate create_posts
CREATE TABLE posts (
  id SERIAL PRIMARY KEY,
  title VARCHAR NOT NULL,
  body TEXT NOT NULL,
  published BOOLEAN NOT NULL DEFAULT FALSE
)


When preparing your app for use in production, you may want to run your migrations during the application’s initialization phase. You may also want to include the migration scripts as a part of your code, to avoid having to copy them to your deployment location/image etc.

The diesel_migrations crate provides the embed_migrations! macro, allowing you to embed migration scripts in the final binary. Once your code uses it, you can simply include connection.run_pending_migrations(MIGRATIONS) at the start of your main function to run migrations every time the application starts.
