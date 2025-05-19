FROM python:3.10

ENV PYTHONUNBUFFERED=1

ENV POSTGRES_SERVER=54.172.230.159
ENV POSTGRES_PORT=5432
ENV POSTGRES_DB="mydb"
ENV POSTGRES_USER="myuser"
ENV POSTGRES_PASSWORD="mypassword"
ENV PROJECT_NAME="Full Stack FastAPI Project"
ENV STACK_NAME=full-stack-fastapi-project

# Backend
#ENV BACKEND_CORS_ORIGINS="http://localhost,http://localhost:5173,http://localhost:5173,http://0.0.0.0:3000,http://54.172.230.159:3000,http://54.172.230.159:5173,http://0.0.0.0:5173,http://localhost.tiangolo.com"
#ENV BACKEND_CORS_ORIGINS="http:///54.172.230.159:8000,http://54.172.230.159:3000,http://54.172.230.159:5173"
ENV SECRET_KEY="khcKmfkSzsSOIylAxyoz0zMX0ieW05a4LBcRoaXMRmA"
ENV FIRST_SUPERUSER=admin@example.com
ENV FIRST_SUPERUSER_PASSWORD="fristproject"

#ENV BACKEND_CORS_ORIGINS="*"



 
WORKDIR /app/

# Install uv
# Ref: https://docs.astral.sh/uv/guides/integration/docker/#installing-uv
COPY --from=ghcr.io/astral-sh/uv:0.5.11 /uv /uvx /bin/

# Place executables in the environment at the front of the path
# Ref: https://docs.astral.sh/uv/guides/integration/docker/#using-the-environment
ENV PATH="/app/.venv/bin:$PATH"

# Compile bytecode
# Ref: https://docs.astral.sh/uv/guides/integration/docker/#compiling-bytecode
ENV UV_COMPILE_BYTECODE=1

# uv Cache
# Ref: https://docs.astral.sh/uv/guides/integration/docker/#caching
ENV UV_LINK_MODE=copy
COPY . . 
# Install dependencies
# Ref: https://docs.astral.sh/uv/guides/integration/docker/#intermediate-layers
#RUN --mount=type=cache,target=/root/.cache/uv \
 #   --mount=type=bind,source=uv.lock,target=uv.lock \
RUN ls -la  #  --mount=type=bind,source=pyproject.toml,target=pyproject.toml \
RUN uv sync --frozen --no-install-project

ENV PYTHONPATH=/app

#COPY ./scripts /app/scripts

#COPY ./pyproject.toml ./uv.lock ./alembic.ini /app/

#COPY ./app /app/app

#COPY . .

# Sync the project
# Ref: https://docs.astral.sh/uv/guides/integration/docker/#intermediate-layers
#RUN --mount=type=cache,target=/root/.cache/uv \
RUN   uv sync

CMD ["fastapi", "run", "--workers", "4", "app/main.py"]
