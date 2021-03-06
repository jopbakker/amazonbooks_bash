# amazon_books
"system" to check for new books from authors

## setup
Build a new container with the dockerfile (executed from the same location as the Dockerfile)
```bash
docker build -t alpine_books .
```

Test the newly made container
```bash
docker run -it --rm alpine_books wget google.com
```
This should generate output showing it performed a wget on google.com


## Testing full system
Create the environment in which to run.
```bash
mkdir books && mv books.sh list.csv books/ && cd books
```
Add proper data the the list.csv
```bash
path=$(pwd)
sed -i 's|author,url|Brandon_Sanderson,https://www.amazon.com/kindle-dbs/entity/author/B001IGFHW6|g' $path"/test.csv"
```

Perform a test run of the container
```bash
path=$(pwd)
docker run -it --name books_check --rm -v $path:/books alpine_books
```

## Automation
Automate as needed
```bash
5 2 * * * docker run -d --name books_check --rm -v ~/books/:/books alpine_books
```
This uses crontab to run this container every day at 2:05 AM
