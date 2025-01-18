FROM python:3.10-slim

COPY ./requirements.txt /requirements/
COPY ./resources/web /web
RUN pip3 install -r /requirements/requirements.txt
ENV PROJECT_HOME=/
EXPOSE 5001
ENTRYPOINT ["python3"]
CMD ["/web/predict_flask.py"]
