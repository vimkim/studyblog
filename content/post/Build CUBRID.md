+++
title = 'Build CUBRID'
date = 2024-04-18T07:24:35+09:08
+++

# 큐브리드 빌드하기

https://www.cubrid.com/blog/3842513

직접 센트OS를 설치하기에는 부담이 있고, 위 글에서 언급된 cubrid-contrib의 sandbox라는 프로그램을 사용해 빌드를 시도했는데, 매우 안정적으로 빌드에 성공했다.


> sandbox 최고


스스로 빌드한 결과 다음과 같은 에러를 마주쳤다.
#### [A manager server process-related error occurs in the execution of the CUBRID source after its build(CUBRIDSUS-3553)](https://www.cubrid.org/manual/en/11.0/release_note/release_note_latest_ver.html#id32)[¶](https://www.cubrid.org/manual/en/11.0/release_note/release_note_latest_ver.html#a-manager-server-process-related-error-occurs-in-the-execution-of-the-cubrid-source-after-its-build-cubridsus-3553 "Permalink to this heading")

If users want to build the CUBRID source and install it themselves, they must build and install CUBRID and the CUBRID Manager respectively. If you check out only CUBRID source and run cubrid service start or cubrid manager start after build, the error “cubrid manager server is not installed” will occur.