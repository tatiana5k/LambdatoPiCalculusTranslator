# LambdaToPiTranslator
A web application that can be used to translate a lambda calculus expression into an equivalent pi calculus expression based on the following model:

<p>
<table style="width:100%">
<tr>
<td><b>Grammar Element</b></td>
<td><b>Lambda Input</b></td>
<td><b>Pi Output</b></td>
</tr>
<tr>
<td>term:</td>
<td>M</td>
<td>[M](p)</td>
</tr>
<tr>
<td>variable:</td>
<td>x</td>
<td>x!p</td>
</tr>

<tr>
<td>expression:</td>
<td>λx M</td>
<td>p?x.p?q.[M](q)</td>
</tr>
<tr>
<td>application:</td>
<td>M N</td>
<td>[M N](p) = new(a).new(b).(([M](a))|(a!b.a!p)|*((b?c).[N](c))</td>
</tr>
</table>

<br>The translator will accept either the lambda character 'λ' or the carat '^' interchangeably. <br>
Abbrevated lambda format is suppoted (eg. λxyz.x y z vs λx.λy.λz.x y z). <br>
Parentheses are supported. <br>
Input Lambda expression MUST use dot notation.<br><br>

<br><br>
Note: The output includes added spaces for improved legibility. Spaces are not specially defined in the Pi grammar.<br>
<hr>
<b>Translation Example: Convert (λx.x) y to Pi</b><br><br>

In simple Pi, using the model described above, the translation is: <br>
[M N](p) = new(a) . new(b) . ( a?x . a?q . x!q | a!b . a!p | *(b?c . y!c))<br><br>

The translator produces: <br>
new(chanA1) . new(chanB1) . (chanA1?x . chanA1?chanQ2 . x!chanQ2 | chanA1!chanB1 . chanA1!topP | *(chanB1?chanC1 . y!chanC1))<br><br>

<hr>

<b>Translation Example: Convert the K combinator λx.(λy. x) to Pi</b><br><br>

In simple Pi, using the model described above, the translation is: <br>
[M N](p) = p?x . p?q . q?y . q?s . x!s <br><br>

The translator produces: <br>
topP?x . topP?chanQ1 . chanQ1?y . chanQ1?chanQ2 . x!chanQ2<br><br>

<hr>

<b>Note: Spaces do matter in the lambda expression input. </b><br>
^x.xy will return a parse error. <br>
^x.x y will parse appropriately: ["LambdaExpr","x",["ApplyExpr",["VarExpr","x"],["VarExpr","y"]]]<br>
and return: topP?x . topP?chanQ1 . new(chanA2) . new(chanB2) . (x!chanA2 | chanA2!chanB2 . chanA2!chanQ1 | *(chanB2?chanC2 . y!chanC2))
^x.(x y) will parse and return the same.<br><br>

(^x.x)y will return a parse error.<br>
(^x.x) y will parse appropreately: ["ApplyExpr",["LambdaExpr","x",["VarExpr","x"]],["VarExpr","y"]]<br>
and return: new(chanA1) . new(chanB1) . (chanA1?x . chanA1?chanQ2 . x!chanQ2 | chanA1!chanB1 . chanA1!topP | *(chanB1?chanC1 . y!chanC1))

<br><br>
<hr>
Lambda to Pi Translator by Tatiana Petkova and Jesse Harder, Copyright 2016, Santa Clara University.<br>
This Translator uses the Jison Javascript Parser Generator and it's Lambda Calculus sample grammar, by Zach Carter, Copyright 2009-2013. MIT Licensed.
<a href="www.jison.org">www.jison.org/</a>


</p>


</body>
</html>
