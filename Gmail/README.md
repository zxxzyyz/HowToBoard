# Gmail

### Filter
1. 보낸 사람 검색
from:
예: from:지현
2. 받는 사람 검색
to:
예: to:인성
3. 메일 사본을 받는 사람 검색
cc:
bcc:
예: cc:인성
4. 제목에 포함된 단어
subject:
예: subject:저녁식사
여러 검색어와 일치하는 메일
OR 또는 { }
예: from:지현 OR from:인성
예: {from:지현 from:인성}
5. 특정 단어가 포함된 결과 제외
-
예: 저녁식사 -영화
6. 근처에 있는 단어로 메일 찾기.
단어와 단어 사이에 들어갈 수 있는 단어 수를 숫자로 지정하세요. 
따옴표를 추가하여 처음에 입력한 단어가 먼저 나오는 메일을 찾습니다.
AROUND
예: 휴일 AROUND 10 휴가
예: "비밀 AROUND 25 생일"
7. 특정 라벨이 있는 메일	
label:
예: label:친구
8. 첨부파일이 있는 메일
has:attachment
예: has:attachment
9. Google 드라이브, 문서, 스프레드시트 또는
프레젠테이션 첨부파일이나 링크가 있는 메일
has:drive
has:document
has:spreadsheet
has:presentation
예: has:drive 
10. YouTube 동영상이 있는 메일
has:youtube
예: has:youtube
11. 메일링 리스트의 메일
list:
예: list:info@example.com
12. 특정 이름 또는 파일 형식의 첨부파일
filename:
예: filename:pdf
예: filename:homework.txt
13. 정확한 단어 또는 문구 검색
" "
예: "오늘 밤 저녁식사와 영화"
14. 여러 개의 검색어 묶기
( )
예: subject:(저녁식사 영화)
15. 스팸 및 휴지통을 포함해 모든 폴더에 있는 메일 검색
in:anywhere
예: in:anywhere 영화
16. 중요 표시된 메일 검색
is:important
label:important
예: is:important
17. 별표편지함, 다시 알림 항목, 읽지않은 메일 또는 읽은 메일
is:starred
is:snoozed
is:unread
is:read
예: is:read is:starred
18. 특정 색상의 아이콘이 포함된 메일	
has:yellow-star
has:blue-info
예: has:purple-star
19. 참조 또는 숨은참조 입력란의 수신자
cc:
bcc:
예: cc:인성
참고: 숨은참조로 받은 메일은 찾을 수 없습니다.
20. 특정 기간에 보낸 메일 검색	
after:
before:
older:
newer:
예: after:2004/04/16
예: before:2004/04/18
21. d(일), m(월), y(연도)를 사용해 특정 기간 이전 또는 이후의 메일 검색	
older_than:
newer_than:
예: newer_than:2d
22. 채팅 메시지
is:chat
예: is:chat 영화
23. 이메일 주소(보낸 메일)
deliveredto:
예: deliveredto:username@gmail.com
24. 특정 카테고리의 메일
category:
예: category:업데이트
25. 특정 크기보다 큰 바이트의 메일
size:
예: size:1000000
26. 특정 크기보다 크거나 작은 바이트의 메일
larger:
smaller:
예: larger:10M
27. 단어와 정확히 일치하는 결과
+
예: +unicorn
28. 특정 메일-ID 헤더가 있는 메일
Rfc822msgid:
예: rfc822msgid:200503292@example.com
29. 라벨이 있거나 없는 메일
has:userlabels
has:nouserlabels
예: has:nouserlabels 
참고: 라벨은 메일에만 추가되며 전체 대화에는 추가되지 않습니다.
