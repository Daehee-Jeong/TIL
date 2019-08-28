## 조회된 데이터에 대한 페이징 구현 시 자주 사용하는 클래스

```java
public class Pagination {
    /** 한 페이지당 게시글 수 **/
    private int pageSize = 10;

    /** 한 블럭(range)당 페이지 수 **/
    private int rangeSize = 10;

    /** 현재 페이지 **/
    private int curPage = 1;

    /** 현재 블럭(range) **/
    private int curRange = 1;

    /** 총 게시글 수 **/
    /*private int listCnt;*/

    /** 총 페이지 수 **/
    private int pageCnt;

    /** 총 블럭(range) 수 **/
    private int rangeCnt;

    /** 시작 페이지 **/
    private int startPage = 1;

    /** 끝 페이지 **/
    private int endPage = 1;

    /** 시작 index **/
    private int startIndex = 0;

    /** 이전 페이지 **/
    private int prevPage;

    /** 다음 페이지 **/
    private int nextPage;

    private Sort sort;

    private String keyword;

    public Pagination(int pageCnt, int curPage, Sort sort, String keyword){

        /**
         * 페이징 처리 순서
         * 1. 총 페이지수
         * 2. 총 블럭(range)수
         * 3. range setting
         */

        /** 현재페이지 **/
        setCurPage(curPage);
        /** 총 게시물 수 **/
        /*setListCnt(listCnt);*/

        /** 1. 총 페이지 수 **/
        setPageCnt(pageCnt);
        /** 2. 총 블럭(range)수 **/
        setRangeCnt(pageCnt);
        /** 3. 블럭(range) setting **/
        rangeSetting(curPage);

        /** DB 질의를 위한 startIndex 설정 **/
        setStartIndex(curPage);

        setSort(sort);

        setKeyword(keyword);
    }

    public String getKeyword() {
        return keyword;
    }

    public void setKeyword(String keyword) {
        if (Objects.isNull(keyword))
            keyword = "";
        this.keyword = keyword;
    }

    public int getPageSize() {
        return pageSize;
    }

    public int getRangeSize() {
        return rangeSize;
    }

    public int getCurPage() {
        return curPage;
    }

    public int getCurRange() {
        return curRange;
    }

    public int getPageCnt() {
        return pageCnt;
    }

    public int getRangeCnt() {
        return rangeCnt;
    }

    public int getStartPage() {
        return startPage;
    }

    public int getEndPage() {
        return endPage;
    }

    public int getStartIndex() {
        return startIndex;
    }

    public int getPrevPage() {
        return prevPage;
    }

    public int getNextPage() {
        return nextPage;
    }

    public String getSort() {
        return sort.toString();
    }

    public void setSort(Sort sort) {
        this.sort = sort;
    }

    public void setCurPage(int curPage) {
        this.curPage = curPage;
    }

    /*public void setListCnt(int listCnt) {
        this.listCnt = listCnt;
    }*/

    public void setPageCnt(int pageCnt) {
        this.pageCnt = pageCnt;
    }
    public void setRangeCnt(int pageCnt) {
        this.rangeCnt = (int) Math.ceil(pageCnt*1.0/rangeSize);
    }
    public void rangeSetting(int curPage){

        setCurRange(curPage);
        this.startPage = (curRange - 1) * rangeSize + 1;
        this.endPage = startPage + rangeSize - 1;

        if(endPage > pageCnt){
            this.endPage = pageCnt;
        }

        this.prevPage = curPage - 1;
        this.nextPage = curPage + 1;
    }
    public void setCurRange(int curPage) {
        this.curRange = (int)((curPage-1)/rangeSize) + 1;
    }
    public void setStartIndex(int curPage) {
        this.startIndex = (curPage-1) * pageSize;
    }
}
```
___

>**수정이력**  
2019.08.28 최초작성