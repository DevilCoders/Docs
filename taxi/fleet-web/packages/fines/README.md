# @yandex-fleet/fines

description(str, argsDescription) {
if (str === undefined && argsDescription === undefined) return this.\_description;
this.\_description = str;
this.\_argsDescription = argsDescription;
return this;
}
