<strong style="line-height: 1.714285714; font-size: 1rem;">Different possible ways of running this class and the results:</strong>

<em>Doing it right, using JAVA_OPTS:</em>

<code><strong>computer$</strong> JAVA_OPTS="-Dproperty1=value1 -Dproperty2=value2 -Dproperty3=value3"<br/>
<strong>computer$</strong> java $JAVA_OPTS JavaOpts101<br/>
Property 1: value1<br/>
Property 2: value2<br/>
Property 3: value3<br/>
</code>

<em>Doing it right, without grouping them in JAVA_OPTS:</em>

<code><strong>computer$</strong> java -Dproperty1=value1 -Dproperty2=value2 -Dproperty3=value3 JavaOpts101<br/>
Property 1: value1<br/>
Property 2: value2<br/>
Property 3: value3<br/>
</code>

<em>Doing it right, grouping two and passing the third one:</em>

<code><strong>computer$</strong> JAVA_OPTS="-Dproperty1=value1 -Dproperty2=value2"<br/>
<strong>computer$</strong> java $JAVA_OPTS -Dproperty3=value3 JavaOpts101<br/>
Property 1: value1<br/>
Property 2: value2<br/>
Property 3: value3<br/>
</code>

<em>So how do you do it wrong?</em>
Basically, you need to be passing the properties in the wrong place, like this:

<code><strong>computer$</strong> JAVA_OPTS="-Dproperty1=value1 -Dproperty2=value2"<br/>
<strong>computer$</strong> java $JAVA_OPTS JavaOpts101 -Dproperty3=value3<br/>
Property 1: value1<br/>
Property 2: value2<br/>
Property 3: null<br/>
</code>

Even if they are grouped on JAVA_OPTS, they won't be correctly passed unless they go before the class name...

<code><strong>computer$</strong> JAVA_OPTS="-Dproperty1=value1 -Dproperty2=value2 -Dproperty3=value3"<br/>
<strong>computer$</strong> java JavaOpts101 $JAVA_OPTS<br/>
Property 1: null<br/>
Property 2: null<br/>
Property 3: null<br/>
</code>

<strong>A little bit of documentation:</strong>

If you do <a href="http://www.manpagez.com/man/1/java/" target="_blank">man java</a> on your command-line and have a read, apart from discovering a new spelling for <em>impletmentations</em> (sic), you'll get something along this:
> SYNOPSIS<br/>
>   java [ options ] class [ argument... ]
>
>   java [ options ] -jar file.jar
>     [ argument... ]
>
> OPTIONS
>
>   -Dproperty=value
>     Sets a system property value.</pre>

<strong>A couple of caveats:</strong>

Notice that you only need to use the quotes when you group the system properties under an environment variable (in these examples, JAVA_OPTS), but you don't need to use the quotes when the properties are passed directly on the command line.
It may be worthy to note here: the order in which the properties are passed <em>among themselves</em> is irrelevant.
