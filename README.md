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

        <form action="#" th:action="@{/saveEmp}" th:object="${user}" method="POST">
    <textarea id="messageInput" class="rounded border border-primary p-5 m-5" style="color: black; background: white; height: 200px; width: 400px; writing-mode: vertical-rl; text-align: right;" maxlength="250"
              th:name="message"
              oninput="limitTextarea(this, 250)"
    ></textarea>
          <span id="charCount" >250</span> characters remaining
          <br>
          <button type="submit" class="btn btn-primary" style="margin-bottom: 70px; font-size: 25px;">إرسال</button>
        </form>

    
