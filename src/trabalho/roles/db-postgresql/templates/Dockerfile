FROM ubuntu:20.04

# Avoid asking for geographic location
ARG DEBIAN_FRONTEND=noninteractive

# Install postgresql
RUN apt-get update && apt-get install -y postgresql postgresql-client libpq-dev postgresql-contrib

# Run the rest of the commands as ``postgres`` user
USER postgres

# Start posgresql service
RUN /etc/init.d/postgresql start

# Activate remote access to database
RUN echo "listen_addresses='*'" >> /etc/postgresql/12/main/postgresql.conf
RUN echo "host all  all    0.0.0.0/0  md5" >> /etc/postgresql/12/main/pg_hba.conf
RUN echo "host all  all    ::/0       md5" >> /etc/postgresql/12/main/pg_hba.conf

# Expose PostgreSQL port
EXPOSE 5432

CMD ["/usr/lib/postgresql/12/bin/postgres", "-D", "/var/lib/postgresql/12/main", "-c", "config_file=/etc/postgresql/12/main/postgresql.conf"]
