```xml
<input type="hidden" id="test_id" class="test_class" name="test_name" value="test">

<script type="text/javascript">
//1. id 로 접근해서 가져오기
var value = $('#test_id').val();
//2. class 로 접근해서 가져오기
var value = $('.test_class').val();
//3. name으로 접근해서 가져오기
var value = $('input[name=test_name]').val();
</script>
```
