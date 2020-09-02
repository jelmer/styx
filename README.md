你好！
很冒昧用这样的方式来和你沟通，如有打扰请忽略我的提交哈。我是光年实验室（gnlab.com）的HR，在招Golang开发工程师，我们是一个技术型团队，技术氛围非常好。全职和兼职都可以，不过最好是全职，工作地点杭州。
我们公司是做流量增长的，Golang负责开发SAAS平台的应用，我们做的很多应用是全新的，工作非常有挑战也很有意思，是国内很多大厂的顾问。
如果有兴趣的话加我微信：13515810775  ，也可以访问 https://gnlab.com/，联系客服转发给HR。
# styx

Export Prometheus data as CSV or directly plot with gnuplot & matplotlib.

## Installation

```
go get -v -u github.com/go-pluto/styx
```

If you want to simply export data from Prometheus as CSV then you don't need to install any thing else.

### Optional Dependencies

If you want to plot directly with gnuplot, you need to install gnuplot first.

#### gnuplot

```bash
brew install gnuplot # macOS
apt-get install gnuplot # Debian / Ubuntu
pacman -S gnuplot # ArchLinux
```

#### matplotlib

```bash
pip install matplotlib
pip2 install matplotlib # macOS
```

## Usage

Once you've [installed](#Installation) styx you can export data.
My recommendation is to actually build the queries in the Prometheus UI
only if you've played with the data there and you know which query is best, 
copy the query and use it to export the data with styx. 

#### CSV

```bash
# export the data for the last hour from http://localhost:9090 
styx 'go_goroutines'
styx 'sum(go_goroutines)'
styx 'go_goroutines{job="prometheus"}'
styx 'go_goroutines > 100'
# export the data for the last 6 hours from http://localhost:9090
styx --duration 6h 'sum(go_goroutines)' 
# export the data from a specific prometheus for the last hour.
styx --prometheus http://prom.example.com 'sum(go_goroutines)' 
```

#### gnuplot

```bash
# plot the data for the last hour from http://localhost:9090
styx gnuplot 'sum(go_goroutines)' > goroutines.gnuplot
# plot the data for the last 6 hours from http://localhost:9090
styx gnuplot --duration 6h 'sum(go_goroutines)' > goroutines.gnuplot 
# plot the data from a specific prometheus for the last hour.
styx gnuplot --prometheus http://prom.example.com 'sum(go_goroutines)' > goroutines.gnuplot
```

Once you have written the generated content into a file you can use this to 
edit and plot the graph:

```bash
gnuplot -p < test.gnuplot
```

#### matplotlib

```bash
# plot the data for the last hour from http://localhost:9090
styx matplotlib 'sum(go_goroutines)' > goroutines.py
# plot the data for the last 6 hours from http://localhost:9090
styx matplotlib --duration 6h 'sum(go_goroutines)' > goroutines.py 
# plot the data from a specific prometheus for the last hour.
styx matplotlib --prometheus http://prom.example.com 'sum(go_goroutines)' > goroutines.py
```

Once you have written the generated content into a file you can use this to 
edit and plot the graph:

```bash
python goroutines.py
```
