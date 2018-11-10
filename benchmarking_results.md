# Results of benchmarking
## Algorithm 1: Recursive merge concat
<table>
  <tr>
    <td rowspan="2"></td>
    <td align="center" colspan="3"><b>Size of Table</b></td>
  </tr>
  <tr>
    <td align="center">100x100 (avg. over 10000 trials)</td>
    <td align="center">1000x1000 (1 trial)</td>
    <td align="center"><code>2**20</code>x<code>2**8</code> (avg. over 3 trials)</td>
  </tr>
  <tr>
  <td>Default Modin (master)</td>
  <td align="center"><code>0.04017304405 s</code></td>
  <td align="center"><code>0.5055962390033528 s</code></td>
  <td align="center"><code>2.0133333333 s</code></td>
  </tr>
  <tr>
    <td>Parallelized Modin</td>
    <td align="center"><code>0.03969048609 s</code></td>
     <td align="center"><code>0.38712550900527276 s</code></td>
     <td align="center"><code>2.49 s</code></td>
  </tr>
  <tr>
    <td align="center"><b>Gain</b></td>
    <td align="center"><b>101.2%</b></td>
    <td align="center"><b>130.6%</b></td>
    <td align="center"><b>80.9%</b></td>
</tr>
</table>
Looking at these results it seems that we are making the system too parallel - the tradeoff between threading overhead and gains from parallelism seems poor for large sizes.

## Algorithm 2: 1 Thread per row concat
### Local CPU:
<table>
<tr>
<td></td>
<td align="center">Size: <code>2**20</code>x<code>2**8</code> (avg. over 3 trials)</td>
</tr>
<tr>
<td>Default Modin (master)</td>
<td align="center"><code>2.22 s</code></td>
</tr>
<tr>
<td>Parallelized Modin</td>
<td align="center"><code>1.59 s</code></td>
</tr>
<tr>
<td align="center"><b>Gain</b></td>
<td align="center"><b>139.6%</b></td>
</tr>
</table>
### Havoc Machine
<table>
<tr>
<td></td>
<td align="center" colspan="2">Size: <code>2**24</code>x<code>2**8</code> (avg. over 7 trials)</td>
</tr>
<tr>
<td></td>
<td align="center">&mu;</td>
<td align="center">&sigma;</td>
</tr>
<tr>
<td>Default Modin (master)</td>
<td align="center"><code>99 s</code></td>
<td align="center"><code>3.88 s</code></td>
</tr>
<tr>
<td>Parallelized Modin</td>
<td align="center"><code>* s</code></td>
<td align="center"><code>* s</code></td>
</tr>
<tr>
<td align="center"><b>Gain</b></td>
<td align="center"><b></b></td>
</tr>
</table>
