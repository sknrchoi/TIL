# URL 관련

## URL.revokeObjectURL()

정적 메서드이며 이전에 URL.createObjectURL()을 통해 생성한 URL객체를 해제한다.  
URL 객체를 더이상 쓸 일이 없을 때 사용하여 브라우저가 객체를 메모리에 들고있지 않도록 하기 때문에,  
객체 할당할 때 항상 이슈가되는 메모리 누수(Memory Leak)를 방지할 수 있다.

```
function downloadBlobData(url) {
    var xhr = new XMLHttpRequest();
    xhr.responseType = 'blob';
    xhr.onload = function () {
        var contentDispo = this.getResponseHeader('Content-Disposition');
        var filename = contentDispo.match(/filename[^;=\n]*=((['"]).*?\2|[^;\n]*)/)[1].replace(/"/gi,'');
        var blob = this.response;
        var a = document.createElement('a');
        a.href = window.URL.createObjectURL(xhr.response);
        a.download = decodeURIComponent(filename);
        a.style.display = 'none';
        document.body.appendChild(a);
        a.click();
        document.body.removeChild(a);
        
        setTimeout(function () { if(downloadUrl) URL.revokeObjectURL(downloadUrl); }, 100);
    };
    xhr.open('GET', url);
    xhr.send();
}

```
