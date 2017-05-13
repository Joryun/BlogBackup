---
title: "Instagram"
noDate: "true"
---
<div class="instagram">
</div>

<script src="js/jquery.lazyload.js"></script>
<script src="js/instagram.min.js"></script>
<script>
jQuery(function($) {
  $('.instagram').on('willLoadInstagram', function(event, options) {
    console.log(options);
  });
  $('.instagram').on('didLoadInstagram', function(event, response) {
    console.log(response);
  });
  $('.instagram').instagram({
    hash: 'perfect',
    clientId: '3ade0267f8cc474fa53686aa6f7a8db5'
  });
});
</script>