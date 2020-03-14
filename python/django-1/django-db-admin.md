# Django DB \(Admin 관련\)

## Admin 페이지 수정

```text
#class ChoiceInline(admin.StackedInline): # 일렬로 보여줌
class ChoiceInline(admin.TabularInline): # Table형식
    model = Choice
    extra =2

class QuestionAdmin(admin.ModelAdmin):
    # 각 필드를 분리해서 보여주려면
    fieldsets = [
        ('Question Statement', {'fields': ['question_text']}),
        ('Date Statement', {'fields': ['pub_date'], 'classes': ['collapse']}),
    ]
    inlines = [ChoiceInline]
    list_display = ('question_text', 'pub_date') # 레코드 리스트 컬럼 지정
    list_filter = ['pub_date'] # 필터 사이드바 추가
    search_fields = ['question_text'] # 검색 박스 추가


# Register your models here.
admin.site.register(Question, QuestionAdmin)
admin.site.register(Choice)
```

## Django shell로 수정

python manage.py shell로 실행

### 데이터 생성 / 입력

```text
from polls.models import Question, Choice
from django.utils import timezone
q = Question(question_text="What's new?", pub_date=timezone.now())
q.save() # save()를 해야 실제 데이터베이스에 적용
```

### 데이터 조회

```text
# 모든 QuerySet 얻기
Question.objects.all() #SELECT

# Filter를 거쳐 원하는 것만 얻기 # WHERE
Question.objects.filter(
    question_text__startswith='what'
).exclude(
    pub_date__gte=datetime.date.today()
).filter(
    pub_date__gte=datetime(2005, 1, 30)
)

# 1개의 확실한 요소 불러오기
one_entry = Question.objects.get(pk=1)

# OFFSET, LIMIT
Question.objects.all()[:5]
Question.objects.all()[5:10]
Question.objects.all()[:10:2]
```

### 데이터 수정

```text
# UPDATE 절
q.question_text = 'What is your favorite hobby?'
q.save()

# 여러 개 한 번에 수정
Question.objects.filter(pub_date__year=2007)
    .update(question_text='Everything is the same')
```

### 데이터 삭제

```text
# DELETE 절
Question.objects.filter(pub_date__year=2005).delete()

# 모든 객체 삭제
Question.objects.all().delete()
```



