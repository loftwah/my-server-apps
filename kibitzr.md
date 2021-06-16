pip install kibitzr

mkdir kzr-example
cd kzr-example
docker run -v $PWD:/root --rm peterdemin/kibitzr init
docker run -v $PWD:/root --rm peterdemin/kibitzr run