# EasyExcel框架

1. 数据导入： 为了防止OOM，EasyExcel使用了inputStream字节流一行一行从磁盘读取
2. 在本项目中，实体类为:
    1. `TrainingPlanSigninVo`
    2. 读取方法为: `EasyExcel.read()`，需要传递三个参数，1、文件流 2、实体类 3、处理读取出来的数据的业务类
    3. 每次读取完都会自动执行`invoke()`方法,在invoke方法里面我们拥有一个data参数，存储本次读取的行的数据，我们可以对数据进行一些校验/存储/过滤操作
    4. 使用`context.readRowHolder().getRowIndex()`用来读取剩余行数量
    5. 最后，和数据库相关的操作(或者任何和服务器压力相关的操作)可以放到`doAfterAllAnalysed()`中，这样可以将多次IO的压力转换成一次
3. 读取方面相对简单，只需要传递三个参数
   ```
   EasyExcel.write(targetFile, LabelExcelRecord.class).sheet("Data").doWrite(labelList);
   ```
   1. 其中，`targetFile`是接受写入的文件，`LabelExcelRecord.class`是写入的实体类型，`labelList`是写入的数据