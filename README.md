# django_opencv
## 예측모델 기반 Face detection 웹서비스
프로젝트 기간: 2024/08/20(화) ~ 2024/08/22(목)  
<br/>

## 개요
이 프로젝트는 Django 웹 프레임워크와 OpenCV 라이브러리를 활용하여 예측모델 기반 얼굴 인식 웹서비스를 구현하는 웹 기반 애플리케이션입니다.  
최근 인공지능(AI) 기술의 발전과 함께 얼굴 인식(Face Detection)은 보안, 출입통제, 사용자 맞춤형 서비스 등 다양한 분야에서 널리 활용되고 있습니다. 특히, 웹서비스에 AI 기술을 접목시키는 수요가 증가함에 따라 AI 모델을 실제 웹 환경에 연동하고 배포하는 실무 능력의 중요성이 커지고 있습니다.  
이 프로젝트는 이러한 기술 흐름에 맞춰, 기계학습 기반 얼굴 인식 기능을 Django 웹 애플리케이션에 통합하고, 이를 실제 사용자에게 서비스 형태로 제공할 수 있도록 설계되었습니다.

**프로젝트 목표**  
이 웹을 통해 사용자가 이미지를 업로드하면, 해당 이미지에서 얼굴을 자동으로 탐지하고 결과를 시각화하여 제공하는 AI 기반 웹 애플리케이션을 구축합니다.  
<br/>

## 사용 기술
- 백엔드 프레임워크: Django
- 이미지 처리: OpenCV
- 웹 배포: PythonAnywhere
- 기타 도구: HTML, CSS, Django Form & ModelForm, FileSystemStorage
<br/>

## 구현 기능
1. Django 프로젝트 및 앱 생성
    - 개발 환경 세팅 및 프로젝트 구조 구성
2. 이미지 업로드 기능 구현
    - 사용자로부터 이미지 파일을 Django Form과 ModelForm을 통해 입력받음
3. 파일 저장 처리
    - 업로드된 파일을 서버의 파일 시스템에 안전하게 저장
4. 얼굴 인식 기능 적용
    - OpenCV를 활용해 이미지에서 얼굴을 탐지
5. 이미지 자동 리사이징
    - 업로드된 이미지를 적절한 크기로 자동 조절
6. 웹서비스 배포
    - PythonAnywhere를 통해 외부 접속이 가능한 웹서비스로 배포
7. 프로젝트 관리 도구 적용
    - requirements.txt, .gitignore 등을 활용한 협업 및 배포 준비
<br/>

## 프로젝트 수행 과정
1. 환경 설정 및 프로젝트 생성
    - OpenCV, Pillow 라이브러리 설치
    - Django 프로젝트와 앱 생성 (cv_project, opencv_webapp)
    - settings.py 기본 설정 수정 (언어, 시간대, 정적 파일, 앱 등록 등)
    - 개발 서버 실행 후 정상 작동 확인

2. Django URL 및 뷰 연결
    - 프로젝트 urls.py에서 앱 URL 포함시키기
    - 앱 내부에 urls.py 생성 후 뷰 연결 (예: index → first_view)
    - 첫 화면 템플릿 생성 및 연결

3. 이미지 파일 업로드를 위한 준비
    - MEDIA_URL, MEDIA_ROOT 설정으로 미디어 파일 저장 경로 지정
    - urls.py에서 미디어 파일 서빙 설정 추가
    - 이미지 업로드용 폼(forms.py) 작성 (제목, 이미지 필드 포함)
    - 업로드 폼 템플릿 생성 (multipart/form-data 포함)

4. 이미지 업로드 처리
    - POST 요청 시 업로드된 이미지와 제목을 받아서 저장
    - FileSystemStorage를 활용해 서버에 이미지 저장 및 URL 생성
    - 저장 후 같은 페이지 혹은 결과 페이지 렌더링

5. ModelForm으로 DB 저장 및 관리
    - 이미지 업로드용 모델 작성 (설명, 파일 경로, 업로드 시간 등)
    - ModelForm 작성으로 DB와 폼 연동
    - 마이그레이션 실행하여 DB에 모델 반영
    - 업로드된 이미지를 DB에 저장하고 템플릿에서 출력

6. OpenCV 얼굴 인식 기능 적용
    - 별도 모듈(cv_functions.py)에 얼굴 및 눈 인식 함수 작성
    - Haar Cascade 모델을 사용해 이미지에서 얼굴과 눈 탐지
    - 인식된 부분에 사각형 표시 후 저장
    - 뷰에서 업로드된 이미지 경로를 받아 얼굴 인식 함수 실행 후 결과 보여주기

7. 이미지 자동 리사이징 기능 추가
    - 업로드된 이미지가 너무 클 경우 비율에 맞춰 크기 조절
    - 얼굴 인식 전에 크기 조절하여 처리 효율 및 결과 개선

8. 관리자 페이지에서 이미지 업로드 모델 관리
    - admin.py에 모델 등록
    - 관리자 페이지에서 업로드된 이미지 및 정보 확인 가능

9. 배포 준비 (PythonAnywhere 등)
    - requirements.txt 생성 (필요 라이브러리 목록)
    - .gitignore 작성 (가상환경, 캐시, DB 등 제외 목록 설정)
    - GitHub에 코드 올리고 관리
<br/>

## 사용한 모델
### OpenCV Haar Cascade 모델
본 프로젝트에서는 OpenCV 라이브러리에서 제공하는 Haar Cascade 분류기를 활용하여 얼굴과 눈을 탐지하였습니다.  
OpenCV에서 제공하는 haarcascade_frontalface_default.xml과 haarcascade_eye.xml 파일을 이용하여 얼굴과 눈 영역을 탐지합니다.  

**특징**  
사전에 학습된 XML 파일 형태의 cascade 분류기를 사용하여, 복잡한 딥러닝 기반 모델 없이도 비교적 간단하게 얼굴 인식 기능을 구현하였습니다.  
컬러 이미지를 그레이스케일로 변환하여 처리 속도를 개선하며, 얼굴과 눈 탐지 시 각각 다른 cascade를 적용하였습니다.  
탐지된 얼굴과 눈 영역에 대해 각각 다른 색으로 사각형 표시를 하여 시각적 피드백을 제공합니다.  
<br/>

## 기존 사이트와 차이점
- **OpenCV + Django의 실질적인 통합**  
단순한 이미지 업로드가 아니라, OpenCV로 실시간 얼굴 및 눈 탐지 처리 후 이미지 반환.  
업로드와 동시에 **자동 이미지 처리(리사이징, 얼굴 탐지 등)** 가 백엔드에서 진행됨.  
<br/>

## 향후 추가할 수 있는 기능
- **OpenCV 기능 확장**  
마스크 착용 여부 감지  
얼굴 인식 후 개인 식별 (Face Recognition)  
객체 감지 (YOLO, SSD, etc.)
- **결과 시각화 강화**  
얼굴 탐지 결과 이미지 외에 탐지 좌표값 출력  
업로드된 이미지 대비 감지된 얼굴 수 표시  
얼굴 영역을 따로 잘라서 썸네일로 저장해 보여주기  

![image](https://github.com/user-attachments/assets/bd2b4d13-394f-4732-b048-2ed11bed8216)
  
![image](https://github.com/user-attachments/assets/aed81e4f-2416-4e72-8c4d-3ce7224c34c2)
