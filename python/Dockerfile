FROM alpine as pull_git

RUN apk add git
RUN echo "version 0.0.1"
RUN git clone https://github.com/kapustina-tatyana/3.2-stock_product_docker.git /stock

FROM python:3.9
WORKDIR /stock
COPY --from=pull_git /stock /stock
ENV SECRET_KEY 'django-verysecure-nw^y+m^wmxza1asgk+)!ua2qx9)g+#v=6%76-9i8i(6eqiw94j'
ENV DEBUG 1
RUN python -m pip install --upgrade pip
RUN ls -lh /stock/
RUN python -m pip install -r requirements.txt
RUN python manage.py migrate
CMD ["gunicorn", "--bind", "0.0.0.0:8000", "stocks_products.wsgi"]