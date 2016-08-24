# Bash Smoothies

## Human readable output of space consumption

See also:[Official Documentation](www.linfo.org/du.html)

du -hs demo-0.0.1-SNAPSHOT.jar

List directory sizes with human readable output
<pre><code>
du -hs *
</code></pre>

List directory sizes & total with human readable output
<pre><code>
du -hsc *
</code></pre>

List files and directories, sort by size and call less
<pre><code>
du -h | sort -n | less
</code></pre>

Provide a list of the names and sizes of directories and files in the current directory that contain the word linux: 
<pre><code>
du -ah | grep linux
</code></pre>

 One way in which du can be used to produce a list of (mostly) directories and files in a directory tree that are consuming large amounts of disk space is to use grep to search for all the lines that contain the upper case letter M (i.e., for megabytes) or G (for gigabytes), such as
 <pre><code>
du -ah | grep M
</code></pre>
