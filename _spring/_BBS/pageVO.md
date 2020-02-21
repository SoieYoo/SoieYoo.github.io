```java
package yoo.homework1.vo;

public class PageVO {

    //한 페이지당 게시되는 게시물 건 수
    private static final int RECORD_COUNT_PER_PAGE =10;

    //페이지 리스트에 게시되는 페이지 건수
    private static final int PAGE_SIZE = 5;

    //현재 페이지 번호
    private int currentPageNo = 1;

    //마지막 페이지 번호
    private int lastPageNo;

    //전체 게시물 건 수
    private int totalRecordCount;

    private int boardNum;

    //이전페이지 화살표
    private boolean prev=false;
    //다음페이지 화살표
    private boolean next=true;

    //현재 페이지 블록
    private int currentBlock;

    //마지막 페이지 블록
    private int lastBlock;

    public int getFirstRecordIndex() {
        int firstRecordIndex = (currentPageNo - 1) * RECORD_COUNT_PER_PAGE;
        if(currentPageNo - 1 < 1) {
            firstRecordIndex = 0;
        }
        return firstRecordIndex;
    }

    public int getCurrentBlock() {
        if(currentPageNo % PAGE_SIZE > 0) {
            this.currentBlock = (currentPageNo / PAGE_SIZE ) + 1;
        } else {
            this.currentBlock = (currentPageNo / PAGE_SIZE);
        }
        return currentBlock;
    }

    public void setCurrentBlock(int currentBlock) {
        this.currentBlock = currentBlock;
    }

    public int getLastBlock() {
        if(totalRecordCount % (PAGE_SIZE * RECORD_COUNT_PER_PAGE) > 0) {
            this.lastBlock = totalRecordCount / (PAGE_SIZE * RECORD_COUNT_PER_PAGE) + 1;
        } else {
            this.lastBlock = (totalRecordCount / PAGE_SIZE * RECORD_COUNT_PER_PAGE);
        }
        return lastBlock;
    }

    public void setLastBlock(int lastBlock) {
        this.lastBlock = lastBlock;
    }

    public boolean isPrev() {
        if(currentPageNo>=0 && currentPageNo<6) {
            setPrev(false);
        }
        else return true;
        return prev;
    }

    public void setPrev(boolean prev) {
        this.prev = prev;
    }

    public boolean isNext() { //수정해야해
        if(getLastBlock()==getCurrentBlock()) {
            setNext(false);
        } else {
            return true;
        }
//        if(getTotalPageCount() <= getCurrentPageNo()) {}
        return next;
    }

    public void setNext(boolean next) {
        this.next = next;
    }

    public int getLastPageNo() {
        if(totalRecordCount % RECORD_COUNT_PER_PAGE > 0) {
            lastPageNo = (totalRecordCount / RECORD_COUNT_PER_PAGE) + 1;
        } else {
            lastPageNo = totalRecordCount / RECORD_COUNT_PER_PAGE;
        }
        return lastPageNo;
    }

    public void setLastPageNo(int lastPageNo) {
        this.lastPageNo = lastPageNo;
    }

    public int getBoardNum() {
        return boardNum;
    }

    public void setBoardNum(int boardNum) {
        this.boardNum = boardNum;
    }

    public int getCurrentPageNo() {
        if(currentPageNo > lastPageNo) {
            currentPageNo = lastPageNo;
        }
        return currentPageNo;
    }

    public void setCurrentPageNo(int currentPageNo) {
        this.currentPageNo = currentPageNo;
    }

    public int getRecordCountPerPage() {
        return RECORD_COUNT_PER_PAGE;
    }

    public int getPageSize() {
        return PAGE_SIZE;
    }

    public int getTotalRecordCount() {
        return totalRecordCount;
    }

    public void setTotalRecordCount(int totalRecordCount) {
        this.totalRecordCount = totalRecordCount;
    }

    public int getTotalPageCount() {
        return ((totalRecordCount - 1) / RECORD_COUNT_PER_PAGE) + 1;
    }

    public int getFirstPageNoOnPageList() {
        return ((currentPageNo - 1) / PAGE_SIZE) * PAGE_SIZE + 1;
    }

    public int getLastPageNoOnPageList() {
        //페이지 리스트의 마지막 페이지 번호 = 페이지 리스트의 첫 페이지 번호 + 페이지 사이즈 5 - 1
        int lastPageNoOnPageList = (getFirstPageNoOnPageList() + PAGE_SIZE - 1);
        if (lastPageNoOnPageList > getTotalPageCount()) {
            lastPageNoOnPageList = getTotalPageCount();
//            lastPageNoOnPageList = lastPageNo;
        }
        return lastPageNoOnPageList;
    }

    public int getLastRecordIndex() {
        return currentPageNo * RECORD_COUNT_PER_PAGE;
    }
}
```
