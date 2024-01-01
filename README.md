# SpringMvc-ThymeLeaf
أكتب ال 
service 
وال
controller
وال 
html
الخاص بعمل 
save on database:

service:
-----------------------------------------------------------
    public User saveUser(User user) {
        return userRepository.save(user);
    }
-------------------------------------------------------------
controller : 
---------------------------------------------------------------
@GetMapping("/saveEmp")
public User saveUser (Model model) {
User user = new User ();
model.addAttribute("user",userService.saveUser(user));
return "redirect:/";
}

    @PostMapping("/saveEmp")
    public String saveEmployee(@ModelAttribute User user) {
        User o = new User ();
        userService.saveUser(o);
        return ("redirect:/");
    }
-------------------------------------------------------------------------

ليس صحيحاً تماماً، إليك التصحيح والإيضاح:

الخطأ:

إنشاء كائن مستخدم فارغ (User o = new User();) ثم تمريره إلى خدمة الحفظ (userService.saveUser(o);). هذا يعني أنك تحفظ كائن مستخدم فارغ، وليس البيانات التي تم إرسالها من نموذج الويب.
التصحيح:

استخدم كائن المستخدم الذي تم تلقيه بالفعل من النموذج باستخدام @ModelAttribute:
Java
@PostMapping("/saveEmp")
public String saveEmployee(@ModelAttribute User user) {
    userService.saveUser(user); // استخدم كائن 'user' الذي يحتوي على البيانات المرسلة
    return "redirect:/";
}
-------------------------------------------------------------------------------------
تستطيع كتابته هكذا زلكن تحتاج لل 
Try catch كي يكتمل
@PostMapping("/saveEmp")
public String saveEmployee(Model model) {
    User user = model.getAttribute("user");

    // Save the user using the service
    userService.saveUser(user);

    // Redirect to the appropriate page
    return "redirect:/";
}
-------------------------------------------------------------------------------
لذلك 
@ModelAttribute 
افضل لك بكثير


----------------------------------------------------------------------------------------------------------------
 HTML
-------------------------------------------------------------------------------------------------------------------
  <form th:action="@{/saveEmp}" th:object="${user}" method="POST">
    <textarea
              th:name="message"  الاشي الوحيد من الاتربيوتس اللي بدك تسيفو
    ></textarea>
          <button type="submit">إرسال</button>
        </form>

    -----------------------------------------------------------------------------
    عرض ال html في صفحة اخرى بعد عملية ال save مرة داخل textArea ومرة داخل ال paraghraph
----------------------------------------------------------------------------------------------
 <textarea th:each="user : ${user}" th:text="${user.message}"></textarea>
paraghraph اما داخل
    <p th:each="user : ${user}" th:text="${user.message}"></p>
    d ولا فيه اي فرق بالمرة
    lبس لازم تنتبه انو في كونترولر بدو يوصلنا لهون عشان نقدرنعمل هاض الحكي

  @GetMapping("/db")
   public String DataBaseTable (Model model){
       model.addAttribute("user",userService.getAllUsers());
       return  "DataBaseTable";
   }
   وبس

@GetMapping("/")
 public String indexPage (){
     return  "index";
 }
    
