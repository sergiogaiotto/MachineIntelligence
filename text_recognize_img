from PIL import Image
import pytesseract
import cv2
from resizeimage import resizeimage
import os
import numpy as np

src_path = '/data/images/'

def get_string(img_path):

    # ler imagem
    img = cv2.imread(img_path)

    # converter para tons de cinza
    img = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)

    # remover ruidos da imagem
    kernel = np.ones((1, 1), np.uint8)
    img = cv2.dilate(img, kernel, iterations=1)
    img = cv2.erode(img, kernel, iterations=1)

    cv2.imwrite(src_path + "removed_noise.png", img)

    # buscar somente itens preto-branco da imagem
    img = cv2.adaptiveThreshold(img, 255, cv2.ADAPTIVE_THRESH_GAUSSIAN_C, cv2.THRESH_BINARY, 11, 2)

    # criar imagem com exemplo de aplicacao do openCV
    cv2.imwrite(src_path + "thres.png", img)

    # reconhecer e extrair texto da imagem
    result = pytesseract.image_to_string(Image.open(src_path + "thres.png"))

    # criacao do arquivo txt com as informacoes
    # os.remove(temp)
    return result



print '--- inicio ---'
print get_string(src_path + "text.jpg")
print "------ fim -------"
