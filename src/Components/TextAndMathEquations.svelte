<script>
  import katexify from "../katexify";

  const math1 = "ax^2+bx+c=0";
  const math2 = "x=-\\frac{-b\\pm\\sqrt{b^2-4ac}}{2a}";
  const math3 = "V=\\frac{1}{3}\\pi r^2 h";

  const mathArray = [math1, math2, math3];
  let index = 0;
  $: math = mathArray[index];

  function changeMath() {
    index = (index + 1) % 3;
  }
</script>
<h1 class="body-header">What makes two players similar?</h1>
<p class="body-text">
The 1990s were a golden age for basketball. The league was expanding and in prime position to gain recognition worldwide. The Chicago Bulls, led by a dominant Michael Jordan, grasped this opportunity and created a dynasty, winning over six championships in nine years. After Jordan retired, many other young players were touted as the next Michael Jordan, and for every player like Kobe Bryant who could live up to this title, fifty more couldn't. To determine whether Anthony Edwards and Michael Jordan are truly similar, we must first define what makes two players similar. The problem here is that every player is unique. Players are an amalgamation of tons of characteristics. No two players are exactly the same. So, how are we going to compare MJ and Ant? For the sake of this project, we will look at these players as they are in-game, ignoring intangibles. That means that we have to access how these players are similar on the basketball court. To do this we will assess what kinds of shots these players take. Where do they like shooting from? Where on the court do they get most of their success? These are the questions we will first look to answer. After that we will access if their shots result in similar levels of scoring. These guys are known scorers, so do they score at the same level across similar stages of their careers? Through the combination of these questions we hope to answer the question of how similar Michael Jordan and Anthony Edwards really are.
</p>

<style>
.body-header {
  text-align: center;
}
</style>