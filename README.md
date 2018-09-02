# [Docker gnuplot](https://hub.docker.com/r/remuslazar/docker-gnuplot/)
[![](https://images.microbadger.com/badges/image/remuslazar/docker-gnuplot.svg)](https://microbadger.com/images/remuslazar/docker-gnuplot "Docker Gnuplot") [![](https://images.microbadger.com/badges/version/remuslazar/docker-gnuplot.svg)](https://microbadger.com/images/remuslazar/docker-gnuplot "Docker Gnuplot")

This is an Alpine Linux based Docker Container to run the latest version of
[gnuplot](http://www.gnuplot.info).

The gnuplot binary is being compiled from source and also configured to use

* gdlib incl. TTF support
* cairo
* lua

Basic TTF fonts like Arial are also included, so the generated e.g. PNGs using
gdlib should look good and without any warnings.

## Usage

```
docker run --rm --volume $(pwd):/work remuslazar/gnuplot your_file.gnu
```

## Example

In this example we will create a very basic data file, simulating a temperature
curve over a period of 24h.

```
# generate some sample data
cat <<EOF > docker-gnuplot-sample-data.csv
20
21
22
21
18
EOF

# generate the plot
docker run --rm --volume $(pwd):/work remuslazar/gnuplot -e \
 "set xlabel 'Sample'; set ylabel 'Temp';
  set term png size 640,300;
  set yrange [0:30];
  set output 'docker-gnuplot-sample-data.png';
  plot 'docker-gnuplot-sample-data.csv' using 0:1 with lines;"
```

This will product a PNG file called `docker-gnuplot-sample-data.png` in the
`cwd`.

## Debugging

To run a shell inside the container:

```
docker run --rm -it --volume $(pwd):/work --entrypoint /bin/sh remuslazar/gnuplot
```

## Author

Remus Lazar (remus at lazar dot info)

## MIT License

See [LICENSE](LICENSE).
