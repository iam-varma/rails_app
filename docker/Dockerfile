# Use an official Ruby runtime as a parent image
FROM ruby:3.1.2

# Install dependencies
RUN apt-get update -qq && apt-get install -y build-essential libpq-dev nodejs

# Set the working directory
WORKDIR /myapp

# Copy the Gemfile and Gemfile.lock
COPY Gemfile Gemfile.lock ./

# Install the gems
RUN gem install bundler:2.3.3
RUN bundle install

# Copy the rest of the application code
COPY . .

#secret key & precompiling the env
ENV SECRET_KEY_BASE=c24e5c548c6b4ab4112cf9739874c035d4e288315fa61096a067ba25f3c33c70b175e8214e853d8e08b2ae6d5f48c834c0e04ed276a1f0134304082d38db27d6
RUN RAILS_ENV=production bundle exec rake assets:precompile

# Expose port 3000 to the Docker host
EXPOSE 3000

# Define the command to run the application
CMD ["bash", "-c", "rm -f tmp/pids/server.pid && rails server -b 0.0.0.0"]

