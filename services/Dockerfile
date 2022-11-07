FROM public.ecr.aws/docker/library/python:3.8-slim as builder
WORKDIR app
COPY .
RUN pip install --user fastapi uvicorn boto3 flask pytest moto
RUN python -m pytest test.py

FROM public.ecr.aws/docker/library/python:3.8-slim as app
WORKDIR app
COPY --from=builder /root/.local /root/.local
COPY --from=builder .
ENV PATH=/root/.local:$PATH
EXPOSE 5000
CMD ["python", "app.py"]