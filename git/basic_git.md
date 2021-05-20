# 기본적인 명령어

## git 시작
```bash
git init
```

## git 상태 확인
```bash
git status
```

## 파일 수정 이력 기록 준비
```bash
git add
```
## 파일 수정 이력 기록 
```bash
git commit
```

## commit 이력 보기
```bash
git log
```

## git 원격 저장소 지정
`origin` 이라는 곳을 `[원격저장소 주소]` 라고 지정 한다
```bash
git remote add origin [원격저장소 주소]
```

## git 프로젝트 원격 저장소에 올리기
origin 원격 저장소에 master 브렌치의 내용을 올리겠다.
`-u` 옵션은 안 넣이도 상관은 없다.
```bash
push -u origin master
```