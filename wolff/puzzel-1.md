<script src="https://cdn.jsdelivr.net/npm/jquery@3.2/dist/jquery.min.js"></script>

# Muziek of niet

Beschrijving…

<div>
  <button onclick="next_animation()">Next animation</button>
  <div id="anim-idx">Animatie X</div>
</div>

<div id="jquery-test"></div>

<script>
  var anim_obj = document.getElementById("anim-idx");
  var count = 0;
  
  function next_animation() {
    anim_obj.innerHTML = "Animatie " + ++count;
  }
  
  $().ready(function() {
    $("#jquery-test").html("Text added by jQuery code.");
  });
</script>
