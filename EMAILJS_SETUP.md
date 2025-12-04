# EmailJS 설정 가이드

이 프로젝트는 EmailJS를 사용하여 문의 폼에서 이메일을 발송합니다. 메일 주소는 EmailJS 대시보드에서 관리되므로 HTML에 노출되지 않습니다.

## 설정 단계

### 1. EmailJS 계정 생성 및 설정

1. [EmailJS](https://www.emailjs.com/)에 가입하거나 로그인합니다.
2. 대시보드로 이동합니다.

### 2. 이메일 서비스 추가

1. **Email Services** 메뉴에서 **Add New Service** 클릭
2. 사용 중인 이메일 서비스 선택 (Gmail, Outlook 등)
3. 서비스 연결 및 인증 완료
4. 생성된 **Service ID**를 복사합니다 (예: `service_xxxxxxx`)

### 3. 이메일 템플릿 생성

1. **Email Templates** 메뉴에서 **Create New Template** 클릭
2. 템플릿 설정:
   - **Template Name**: Contact Form (또는 원하는 이름)
   - **Subject**: `문의: {{from_name}}`
   - **Content**:
     ```
     이름: {{from_name}}
     이메일: {{from_email}}
     회사명: {{company}}
     
     메시지:
     {{message}}
     ```
   - **To Email**: 받을 이메일 주소 입력 (여기에 실제 메일 주소를 입력)
   - **From Name**: {{from_name}}
   - **Reply To**: {{from_email}}
3. **Save** 클릭
4. 생성된 **Template ID**를 복사합니다 (예: `template_xxxxxxx`)

### 4. Public Key 확인

1. **Account** 메뉴로 이동
2. **General** 탭에서 **Public Key**를 복사합니다 (예: `xxxxxxxxxxxxx`)

### 5. HTML 파일에 설정 적용

`index.html` 파일을 열고 다음 부분을 찾아서 실제 값으로 교체하세요:

```javascript
const EMAILJS_SERVICE_ID = 'YOUR_SERVICE_ID'; // 여기에 Service ID 입력
const EMAILJS_TEMPLATE_ID = 'YOUR_TEMPLATE_ID'; // 여기에 Template ID 입력
const EMAILJS_PUBLIC_KEY = 'YOUR_PUBLIC_KEY'; // 여기에 Public Key 입력
```

예시:
```javascript
const EMAILJS_SERVICE_ID = 'service_abc123';
const EMAILJS_TEMPLATE_ID = 'template_xyz789';
const EMAILJS_PUBLIC_KEY = 'abcdefghijklmnop';
```

## 무료 플랜 제한

- 월 200건의 이메일 전송
- 충분하지 않다면 유료 플랜으로 업그레이드 가능

## 보안 참고사항

- Public Key는 클라이언트에 노출되어도 안전합니다
- 실제 이메일 주소는 EmailJS 대시보드의 템플릿 설정에서만 관리됩니다
- HTML 소스 코드에는 이메일 주소가 노출되지 않습니다

## 문제 해결

### 이메일이 전송되지 않는 경우

1. Service ID, Template ID, Public Key가 올바른지 확인
2. EmailJS 대시보드의 **Logs** 메뉴에서 에러 확인
3. 브라우저 콘솔에서 JavaScript 에러 확인
4. 이메일 서비스 연결 상태 확인

### 스팸 폴더에 들어가는 경우

- EmailJS에서 발송된 이메일이 스팸으로 분류될 수 있습니다
- 받는 이메일 주소에서 EmailJS 도메인을 허용 목록에 추가하세요

