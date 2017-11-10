# zhuzhengqi_h_s
#coding:utf-8
# 计算主蒸汽、一抽、冷再的蒸汽焓值、熵值，绘制曲线

import xlrd
import numpy as np
import scipy
from iapws import IAPWS97
import matplotlib.pyplot as plt

hst = np.zeros((3,2))

workbook = xlrd.open_workbook('ge_duan_chou_qi.xls')
worksheet = workbook.sheet_by_index(0)

zzq_p = worksheet.cell_value(0,0)
zzq_t = worksheet.cell_value(0,1)
ydcq_p = worksheet.cell_value(0,2)
ydcq_t = worksheet.cell_value(0,3)
edcq_p = worksheet.cell_value(0,4)
edcq_t = worksheet.cell_value(0,5)

zzq_cs = IAPWS97(P = zzq_p, T = zzq_t+273.15 )
ydcq_cs = IAPWS97(P = ydcq_p, T = ydcq_t+273.15 )
edcq_cs = IAPWS97(P = edcq_p, T = edcq_t+273.15 )

hst[0,0] = zzq_cs.h
hst[0,1] = zzq_cs.s
hst[1,0] = ydcq_cs.h
hst[1,1] = ydcq_cs.s
hst[2,0] = edcq_cs.h
hst[2,1] = edcq_cs.s

print(hst)
