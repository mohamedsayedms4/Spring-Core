🔍 ما هو AOP؟
AOP أو البرمجة الموجهة للجوانب (Aspect Oriented Programming) هي نمط برمجي يتيح فصل المهام المشتركة (مثل الـ Logging، الأمان، التحقق من الصلاحيات، التعامل مع المعاملات...) عن منطق العمل الأساسي (Business Logic) بدون تكرار الكود.

🧠 لماذا نستخدم AOP؟
✅ فصل الاهتمامات (Separation of Concerns)

✅ تقليل تكرار الكود (DRY)

✅ تسهيل الصيانة والتطوير

✅ إمكانية التحكم في الكود بدون تعديله مباشرة

🧩 أهم المفاهيم في AOP
المصطلح	الشرح
Aspect	كود يحتوي منطق مشترك يتم تطبيقه (مثل Logging)
Join Point	نقطة في التنفيذ يمكن فيها إدخال كود إضافي (مثل استدعاء ميثود)
Advice	الكود الذي سيتم تنفيذه عند نقطة معينة
Pointcut	تعبير يحدد أين يتم تنفيذ الـ Advice
Weaving	عملية دمج الـ Aspect مع الكود الأساسي

🛠️ أنواع Advice في Spring AOP
النوع	التوقيت	الشرح
@Before	قبل تنفيذ الميثود	
@After	بعد تنفيذ الميثود (بغض النظر عن النتيجة)	
@AfterReturning	بعد التنفيذ الناجح	
@AfterThrowing	عند حصول استثناء	
@Around	قبل وبعد التنفيذ + إمكانية التحكم الكامل	

🧪 مثال عملي
1️⃣ كلاس الهدف:
java
Copy
Edit
@Component
public class StudentService {
    public void printData() {
        System.out.println("عرض بيانات الطالب");
    }
}
2️⃣ كلاس الـ Aspect:
java
Copy
Edit
@Aspect
@Component
public class LoggingAspect {

    @Before("execution(* printData(..))")
    public void beforeAdvice() {
        System.out.println("📍 سيتم تنفيذ الدالة الآن...");
    }

    @After("execution(* printData(..))")
    public void afterAdvice() {
        System.out.println("📍 تم تنفيذ الدالة.");
    }
}
3️⃣ تكوين الحاوية:
java
Copy
Edit
@Configuration
@ComponentScan(basePackages = "com.example")
@EnableAspectJAutoProxy
public class SpringConfig {
}
4️⃣ Main:
java
Copy
Edit
public class Main {
    public static void main(String[] args) {
        AnnotationConfigApplicationContext context =
                new AnnotationConfigApplicationContext(SpringConfig.class);

        StudentService service = context.getBean(StudentService.class);
        service.printData();

        context.close();
    }
}
🧩 أشهر تعبيرات Pointcut
التعبير	المعنى
execution(* package.Class.method(..))	دالة معينة
within(package..*)	كل دوال باكيج معين
@annotation(...)	دوال تحمل أنوتيشن معين
args(..)	حسب نوع باراميترات الدالة
bean(beanName)	حسب اسم الـ Bean

📌 الأنوتيشن المستخدمة في Spring AOP
الأنوتيشن	الوظيفة
@Aspect	تعريف كلاس كـ Aspect
@Before	تنفيذ قبل الدالة
@After	تنفيذ بعد الدالة
@AfterReturning	تنفيذ بعد النجاح
@AfterThrowing	تنفيذ عند الخطأ
@Around	تنفيذ شامل وتحكم كامل
@Pointcut	تعريف نقطة تنفيذ خاصة
@EnableAspectJAutoProxy	تفعيل دعم AOP في Spring

🎯 متى تستخدم AOP؟
عند وجود منطق متكرر في أكثر من مكان مثل:

تسجيل الدخول (Logging)

التحقق من الصلاحيات

المعاملات (Transactions)

التعامل مع الاستثناءات

الأداء (Performance monitoring)

💬 الخلاصة
AOP هي أداة قوية بتوفرها Spring عشان تفصل المنطق المكرر عن الكود الأساسي، وبتخلي المشروع أنظف وأسهل في الصيانة والتوسعة.
