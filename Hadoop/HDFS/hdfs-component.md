# Namenode, Datanode, FsImage, EditLog
> Backlink: [HDFS Home](/Hadoop/HDFS/README.md)

## 도서관 이용하는 사용자

![alt text](/asset/librarian.png)

1. 사용자는 사서에게 책을 요청(대여, 반납)하고 사서는 책장에서 요청을 처리.
2. 사서는 책장에서 변경된 내용(책의 위치 변경, 삭제 등)을 업무용 다이어리에 기록
3. 도서관 마감시간이 되거나 일정 시간 이후 사서는 다이어리의 내용을 토대로 카탈로그를 업데이트

## HDFS 이용하는 사용자

![alt text](/asset/hdfs-lifecycle.png)

1. 사용자는 Namenode에게 데이터를 요청
2. Namenode는 Datanode에게 사용자가 요청한 데이터 읽기/쓰기를 지시
3. 모든 요청을 처리 후 데이터의 변경된 상태를 EditLog에 기록
4. 일정 시간 이후 EditLog의 기록을 FsImage에 모두 병합

## Namenode, Datanode, FsImage, EditLog

![alt text](/asset/hdfs-architecture-1.png)

- Namenode
    - 개념: HDFS의 Masternode
    - 특징
        - 실제 파일을 저장하지 않고, 메타데이터를 관리.
        - 1대의 Namenode에서 여러 대의 Datanode관리하기 때문에 **SPOF(Single Point of Failure)** 발생할 가능성 있음.
- Datanode
    - 개념: 데이터를 실제 저장하고 관리.
    - 특징
        - 블록 단위로 데이터를 저장하고, Namenode의 지시를 받아 데이터를 읽고 씀.
        - Namenode에게 주기적으로 **Heartbeat(생체주기)**와 **Block report(블록보고서)**를 전달하여 자신의 상태와 블록 정보를 알려줌.
- FsImage
    - 개념: HDFS의 전체 상태를 메타데이터로 기록하고 관리하기 위한 파일.
    - 특징
        - HDFS가 시작될 때 FsImage를 확인하여 메타데이터를 파악
- EditLog
    - 개념: 데이터를 읽고 쓸 때 변경사항을 기록하는 파일.
    - 특징
        - 실시간으로 변경되는 사항을 기록.
        - Checkpointing을 통해 EditLog의 상태를 FsImage에 병합 후 기록.