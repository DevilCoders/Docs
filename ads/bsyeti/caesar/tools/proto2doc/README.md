# Print Profile Protos
Тулза для рекурсивной печати схемы протобуфов с вложенными сообщениями.  
Пример вывода тулзы:
```proto
message NCSR.TBannerProfileProto {
	optional uint64 BannerID = 1 [(.NCSR.FieldName) = "BannerID", (.NCSR.FieldType) = PFT_KEY];
	optional uint64 AliveTimeStamp = 2 [(.NCSR.FieldName) = "AliveTimeStamp", (.NCSR.FieldType) = PFT_SIMPLE, (.NCSR.Aggregate) = "max"];
	optional .NCSR.TServiceFields ServiceFields = 9; CONSISTS OF [
		optional .NCSR.EProfileServiceFlags Flags = 1; CONSISTS OF [
			enum EProfileServiceFlags {
			  PSF_NONE = 0;
			  PSF_DELETED = 1;
			  PSF_FULL = 2;
			}
		]
		optional fixed64 ChangedColumns = 2;
	]
}
```
В файле main.cpp подключены все заголовки протобуфов из директории caesar/libs/profiles/proto.  
В функции main определяется набор дескрипторов сообщений протобуфов, которые добавляются в вектор.
Объект TProtoPrinter обрабатывает по одному дескриптору потокобезопасно и осуществляет вывод в  
ту же директорию в файл с названием как у обрабатываемого мессаджа.
```bash
Usage: ./proto2doc [OPTIONS]

Options:
  --svnrevision           print svn version
  {-?|--help}             print usage
  {-O|--output-file} <string>
                          Print all messages to single file
  {-D|--output-dir} <string>
                          Print each message to own file in directory
  {-F|--format} <EFormat> Output file format
  {-C|--collapsed} <ECollapsed>
                          Hide each message fields under the hood (only for rich
                          formats).
```
