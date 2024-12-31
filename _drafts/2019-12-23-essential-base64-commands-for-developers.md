---
layout: post
title: "Essential Base64 Commands For Developers"
author: andre
categories: [ bash ]
tags: [bash, base64, terminal]
image: /assets/images/feature-images/feature-image-bash.jpg
description: This post provides a quick reference to the base64 commands that I use on macOS. The base64 command encodes and decodes Base64 data, as specified in RFC 4648.
comments: true
---

- Table of Contents
{:toc .large-only}

This post provides a quick reference to the base64 commands that I use on macOS. This is not a complete set of base64 commands with detailed explanations on what each command does. If you want to read detailed documentation on the different options and arguments of the base64 command, please refer to the *man* pages of the base64 command. 

The base64 command encodes and decodes Base64 data, as specified in RFC 4648. With no options, the base64 commands reads raw data from stdin and writes encoded data as a continuous block to stdout.

## What is Base64?
The Base 64 encoding is designed to represent arbitrary sequences of octets in a form that allows the use of both upper- and lowercase letters but that need not be human readable. A 65-character subset of US-ASCII is used, enabling 6 bits to be represented per printable character. (The extra 65th character, "=", is used to signify a special processing function.) ~ [RFC4648][1] 

## How does Base64 Work?
The encoding process represents 24-bit groups of input bits as output strings of 4 encoded characters.  Proceeding from left to right, a 24-bit input group is formed by concatenating 3 8-bit input groups. These 24 bits are then treated as 4 concatenated 6-bit groups, each of which is translated into a single character in the base 64 alphabet. Each 6-bit group is used as an index into an array of 64 printable characters.  The character referenced by the index is placed in the output string. ~ [RFC4648][1]

<br/>
<iframe width="800" height="450" src="https://www.youtube.com/embed/aUdKd0IFl34" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
<br/>

## Index Table
The Base64 index table looks as follows: 

<table style="text-align:center">

<tbody><tr>
<th scope="col">Index</th>
<th scope="col">Binary</th>
<th scope="col">Char
</th>
<td rowspan="17">
</td>
<th scope="col">Index</th>
<th scope="col">Binary</th>
<th scope="col">Char
</th>
<td rowspan="17">
</td>
<th scope="col">Index</th>
<th scope="col">Binary</th>
<th scope="col">Char
</th>
<td rowspan="17">
</td>
<th scope="col">Index</th>
<th scope="col">Binary</th>
<th scope="col">Char
</th></tr>
<tr>
<td>0</td>
<td>000000</td>
<td><code>A</code></td>
<td>16</td>
<td>010000</td>
<td><code>Q</code></td>
<td>32</td>
<td>100000</td>
<td><code>g</code></td>
<td>48</td>
<td>110000</td>
<td><code>w</code>
</td></tr>
<tr>
<td>1</td>
<td>000001</td>
<td><code>B</code></td>
<td>17</td>
<td>010001</td>
<td><code>R</code></td>
<td>33</td>
<td>100001</td>
<td><code>h</code></td>
<td>49</td>
<td>110001</td>
<td><code>x</code>
</td></tr>
<tr>
<td>2</td>
<td>000010</td>
<td><code>C</code></td>
<td>18</td>
<td>010010</td>
<td><code>S</code></td>
<td>34</td>
<td>100010</td>
<td><code>i</code></td>
<td>50</td>
<td>110010</td>
<td><code>y</code>
</td></tr>
<tr>
<td>3</td>
<td>000011</td>
<td><code>D</code></td>
<td>19</td>
<td>010011</td>
<td><code>T</code></td>
<td>35</td>
<td>100011</td>
<td><code>j</code></td>
<td>51</td>
<td>110011</td>
<td><code>z</code>
</td></tr>
<tr>
<td>4</td>
<td>000100</td>
<td><code>E</code></td>
<td>20</td>
<td>010100</td>
<td><code>U</code></td>
<td>36</td>
<td>100100</td>
<td><code>k</code></td>
<td>52</td>
<td>110100</td>
<td><code>0</code>
</td></tr>
<tr>
<td>5</td>
<td>000101</td>
<td><code>F</code></td>
<td>21</td>
<td>010101</td>
<td><code>V</code></td>
<td>37</td>
<td>100101</td>
<td><code>l</code></td>
<td>53</td>
<td>110101</td>
<td><code>1</code>
</td></tr>
<tr>
<td>6</td>
<td>000110</td>
<td><code>G</code></td>
<td>22</td>
<td>010110</td>
<td><code>W</code></td>
<td>38</td>
<td>100110</td>
<td><code>m</code></td>
<td>54</td>
<td>110110</td>
<td><code>2</code>
</td></tr>
<tr>
<td>7</td>
<td>000111</td>
<td><code>H</code></td>
<td>23</td>
<td>010111</td>
<td><code>X</code></td>
<td>39</td>
<td>100111</td>
<td><code>n</code></td>
<td>55</td>
<td>110111</td>
<td><code>3</code>
</td></tr>
<tr>
<td>8</td>
<td>001000</td>
<td><code>I</code></td>
<td>24</td>
<td>011000</td>
<td><code>Y</code></td>
<td>40</td>
<td>101000</td>
<td><code>o</code></td>
<td>56</td>
<td>111000</td>
<td><code>4</code>
</td></tr>
<tr>
<td>9</td>
<td>001001</td>
<td><code>J</code></td>
<td>25</td>
<td>011001</td>
<td><code>Z</code></td>
<td>41</td>
<td>101001</td>
<td><code>p</code></td>
<td>57</td>
<td>111001</td>
<td><code>5</code>
</td></tr>
<tr>
<td>10</td>
<td>001010</td>
<td><code>K</code></td>
<td>26</td>
<td>011010</td>
<td><code>a</code></td>
<td>42</td>
<td>101010</td>
<td><code>q</code></td>
<td>58</td>
<td>111010</td>
<td><code>6</code>
</td></tr>
<tr>
<td>11</td>
<td>001011</td>
<td><code>L</code></td>
<td>27</td>
<td>011011</td>
<td><code>b</code></td>
<td>43</td>
<td>101011</td>
<td><code>r</code></td>
<td>59</td>
<td>111011</td>
<td><code>7</code>
</td></tr>
<tr>
<td>12</td>
<td>001100</td>
<td><code>M</code></td>
<td>28</td>
<td>011100</td>
<td><code>c</code></td>
<td>44</td>
<td>101100</td>
<td><code>s</code></td>
<td>60</td>
<td>111100</td>
<td><code>8</code>
</td></tr>
<tr>
<td>13</td>
<td>001101</td>
<td><code>N</code></td>
<td>29</td>
<td>011101</td>
<td><code>d</code></td>
<td>45</td>
<td>101101</td>
<td><code>t</code></td>
<td>61</td>
<td>111101</td>
<td><code>9</code>
</td></tr>
<tr>
<td>14</td>
<td>001110</td>
<td><code>O</code></td>
<td>30</td>
<td>011110</td>
<td><code>e</code></td>
<td>46</td>
<td>101110</td>
<td><code>u</code></td>
<td>62</td>
<td>111110</td>
<td><code>+</code>
</td></tr>
<tr>
<td>15</td>
<td>001111</td>
<td><code>P</code></td>
<td>31</td>
<td>011111</td>
<td><code>f</code></td>
<td>47</td>
<td>101111</td>
<td><code>v</code></td>
<td>63</td>
<td>111111</td>
<td><code>/</code>
</td></tr>
<tr>
<td colspan="2" data-sort-value="" style="background: #ececec; color: #2C2C2C; vertical-align: middle; text-align: center;" class="table-na">Padding</td>
<td>=</td>
<td colspan="12">
</td></tr></tbody></table>
<br/>

## Command Examples
---
### 1. Help and Information Commands
To find help or learn more about the different options and arguements used as part of the base64 command, you can type the following in the terminal console.

**Command:**
```bash
# Display quick help information about the base64 command
$ base64 --help
```

---
### 2. Encode Raw Message (STDIN)
The base64 commands reads raw data from stdin and writes encoded data as a continuous block to stdout.

**Command:**
```bash
# Read raw data from stdin and write encoded data to stdout
$ echo 'Hello World' | base64
```

---
### 3. Decode Encoded Message (STDIN)
The base64 commands reads encoded data from stdin and writes decoded data as a continuous block to stdout.

**Command:**
```bash
# Read raw data from stdin and write encoded data to stdout
$ echo 'SGVsbG8gV29ybGQK' | base64 --decode
```

---
### 4. Encode Raw Message (Files)
The base64 commands reads raw data from an input file and writes encoded data as a continuous block to an output file.

**Command:**
```bash
# Read raw data from input file and write encoded data to output file.
$ base64 -i raw_message.txt -o encoded_message.txt
```

---
### 5. Decode Encoded Message (Files)
The base64 commands reads encoded data from an input file and writes decoded data as a continuous block to an output file.

**Command:**
```bash
# Read encoded data from input file and write decoded data to output file.
$ base64 -d -i encoded_message.txt -o decoded_message.txt
```

## Summary
The base64 commands listed in this article is by no means a complete set of base64 command and only serve as a quick reference to be used by developers. To see the full documentation of the base64 command, please read the *man* pages of the base64 command.

Follow me on any of the different social media platforms and feel free to leave comments.

[1]:https://tools.ietf.org/html/rfc4648